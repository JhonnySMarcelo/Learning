- Injeção de Dependência (Dependency Injection)
	- Conceito e importância da Injeção de Dependência: Injeção de Dependência (DI) é um padrão de design que permite aumentar a modularidade e facilitar o gerenciamento de dependências entre objetos. Em vez de um objeto instanciar diretamente suas dependências, essas são injetadas ou fornecidas a ele de fora, geralmente em um contêiner de DI, tornando o código mais testável e desacoplado. A DI reduz o acoplamento entre classes e facilita a substituição de implementações (como em testes unitários com mocks). A Injeção de Dependência está relacionada ao padrão de Inversão de Controle  (Inversion of Control - IoC), mas não são sinônimos.
	- Tempo de vida (Lifetime) 
		- Transient: Um serviço é criado toda vez que ele é solicitado. Ou seja, sempre que o serviço é injetado em um controlador ou classe, uma nova instância é criada. É ideal para serviços que precisam ser leves e que não compartilham dados ou estado entre diferentes partes da aplicação.
		
		- Scoped: Um serviço é criado para cada requisição. Apenas uma instância do serviço é criada e compartilhada por toda a requisição. Ideal para serviços que precisam compartilhar estado ou dados durante uma requisição. Como serviços WEB e transações de banco de dados.
		
		- Singleton: Um serviço é criado para toda a aplicação. A mesma instância é compartilhada entre todas as requisições e classes durante o tempo de vida da aplicação. É ideal para serviços que têm um alto custo de criação e/ou são eficientes quando reutilizados. Atenção ao usar com dependências que não são thread-safe, pois a instância será acessada por diferentes requisições simultaneamente. É uma boa prática a utilização em serviços de log.
		
		Exemplo de registro dos 3 Tempos de Vida de dependências no container interno de injeção de dependência do .NET na classe Startup/Program, onde deve se registrar a interface que será injetada junto com a classe que contém sua implementação:
		```csharp
		public void ConfigureServices(IServiceCollection services)
		{
			services.AddTransient<IMyDependencyA, MyDependencyA>();
			services.AddSingleton<IMyDependencyB, MyDependencyB>();
			services.AddScoped<IMyDependencyC, MyDependencyC>();
		}
		```
	- Tipos de Injeção de Dependência 
		- Injeção de Dependência por interface: A injeção por interface é o ato de se utilizar a interface ao invés de uma classe concreta ao realizar a DI. Assim permitindo desacoplamento entre a classe dependente e sua implementação concreta. Essa forma pode ser utlizada via construtor ou via propriedade, sendo a DI por interface a mais recomendada, pois facilita a troca de implementação em tempo de execução e facilita a implementação de testes na aplicação.
		
		- Injeção via Construtor (Constructor): A forma mais comum de injeção e a mais recomendada, onde as dependências são passadas como parâmetros no construtor da classe. Ela permite que as dependências sejam obrigatórias, pois a classe não pode ser instanciada sem elas. É a mais utilizada, especialmente por ser compatível com Injeção de Dependência automática em frameworks como o ASP.NET Core.
		```csharp
		public interface ILogger
		{
			void Log(string message);
		}

		public class ConsoleLogger : ILogger
		{
			public void Log(string message)
			{
				Console.WriteLine(message);
			}
		}

		public class MyService
		{
			private readonly ILogger _dependency;
			public MyService(ILogger dependency)
			{
				_dependency = dependency;
			}

			public void DoWork()
			{
				_dependency.Log("Executando...");
			}
		}
		```
		Registro no container:
		```csharp
		// Registro da interface e da classe que a implementa
		builder.Services.AddSingleton<ILogger, ConsoleLogger>();
	
		// Registro da classe dependente para o container resolver as DI automaticamente
		builder.Services.AddSingleton<MyService>();
		```
	
		Também é possível fazer a injeção da dependência utilizando uma classe concreta ao invéz da interface, ESSA NÃO É A FORMA RECOMENDADA, pois dessa forma é criada um acoplamento mais forte comparado ao uso de interface.
						
	    Exemplo de Injeção via Construtor (Constructor) utilizando classe concreta:
		```csharp
		public class ConsoleLogger
		{
			public void Log(string message)
			{
				Console.WriteLine(message);
			}
		}

		public class MyService
		{
			private readonly ConsoleLogger _dependency;

			// Injeção via construtor sem interface
			public MyService(ConsoleLogger dependency)
			{
				_dependency = dependency;
			}

			public void DoWork()
			{
				_dependency.Log("Executando...");
			}
		}
		```
		Registro no container:
		```csharp	
		// Registro da classe dependente e da classe concreta para o container resolver as DI automaticamente
		builder.Services.AddSingleton<ConsoleLogger>();
		builder.Services.AddSingleton<MyService>();
		```
	
		- Injeção via Propriedade (Setter): A injeção da dependência é realizada por uma propriedade pública. A diferença entre esta e a via construtor é o fato da a dependência ser injetada apenas após a criação do objeto e não no momento da criação. Nessa forma de ID existe uma classe dependente que contém a propriedade pública para receber a dependência.
		```csharp
		public interface ILogger
		{
			void Log(string message);
		}

		public class ConsoleLogger : ILogger
		{
			public void Log(string message)
			{
				Console.WriteLine(message);
			}
		}

		public class MyService
		{
			// Propriedade que recebe a dependência através de um setter
			public ILogger dependency  { get; set; }

			public void DoWork()
			{
				dependency.Log("Executando...");
			}
		}
		
		// Chama da classe com injeção por Setter
		_myService.dependency = new ConsoleLogger(); 
		_myService.DoWork()
		```
			
		Também é possível fazer a injeção da dependência via Setter utilizando uma clase concreta ao invez de uma interface, ESSA NÃO É A FORMA RECOMENDADA:
		```csharp
		public class ConsoleLogger
		{
			public void Log(string message)
			{
				Console.WriteLine(message);
			}
		}

		public class MyService
		{
			// Propriedade concreta, não interface (não recomendado)
			public ConsoleLogger dependency { get; set; } 

			public void DoWork()
			{
				dependency.Log("Executando...");
			}
		}
		```

		Em ambas opções (interface ou classe concreta), é possível manter a propriede privada e receber a DI através de um método público.
		# Comparação entre Métodos de Injeção de Dependência

		| Característica                        | Injeção via Construtor                     | Injeção via Propriedade (Setter)            |
		|---------------------------------------|--------------------------------------------|---------------------------------------------|
		| **Momento da Injeção**                | No momento da criação da instância         | Após a criação da instância                 |
		| **Obrigatoriedade da dependência**    | Sim, a dependência é obrigatória           | Não, a dependência pode ser opcional        |
		| **Testabilidade**                     | Alta, fácil de mockar dependências         | Média, pode ser testável, mas depende da atribuição manual |
		| **Facilidade de uso em DI automática**| Totalmente suportado                       | Suportado, mas menos comum                  |
		| **Vantagens**                         | Torna dependências obrigatórias e explícitas, fácil integração com containers de DI | Flexível, dependências podem ser injetadas depois |
		| **Desvantagens**                      | Não permite dependências opcionais sem sobrecarga de construtores | Pode deixar dependências não inicializadas, causando erros em tempo de execução |
	- Implementação de Injeção de Dependência em C# (🚧)
	- Frameworks de Injeção de Dependência (Autofac, Microsoft DI, etc.) (🚧)