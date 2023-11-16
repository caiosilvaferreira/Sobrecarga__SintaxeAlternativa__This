# Sobrecarga, sintaxe alternativa e this

# Sobrecarga

A sobrecarga de métodos é uma técnica de programação em que um mesmo método pode ter diferentes implementações, com diferentes parâmetros de entrada. Em C#, é possível criar métodos sobrecarregados usando o mesmo nome para cada um deles, desde que tenham assinaturas de parâmetros diferentes. A assinatura de um método é composta pelo nome do método e pelos tipos e ordem dos parâmetros que ele recebe.

Por exemplo, o código abaixo mostra duas implementações sobrecarregadas do método `Soma`, que recebe dois inteiros como parâmetros:

```
public int Soma(int a, int b)
{
  return a + b;
}

public int Soma(int a, int b, int c)
{
  return a + b + c;
}

```

Nesse caso, temos dois métodos com o mesmo nome `Soma`, mas com assinaturas de parâmetros diferentes. O primeiro método recebe dois inteiros e retorna a soma deles, enquanto o segundo método recebe três inteiros e retorna a soma dos três.

Ao chamar o método `Soma`, o compilador do C# identifica qual das implementações deve ser usada com base nos tipos e na ordem dos parâmetros passados. Por exemplo, ao chamar `Soma(2,3)`, o compilador usa a primeira implementação, enquanto ao chamar `Soma(2,3,4)`, ele usa a segunda implementação.

A sobrecarga de métodos é uma técnica útil para criar métodos que executam tarefas similares, mas com parâmetros diferentes. Ela torna o código mais legível e fácil de manter, pois evita a criação de métodos com nomes diferentes para tarefas similares.

codigos que mexi antes e depois da sobrecarga

antes:

```csharp
using System;
using System.Globalization;
namespace Course {
    class Program {
        static void Main(string[] args) {
           
            

            Console.WriteLine("Entre os dados do produto:");
            Console.Write("Nome: ");
            string Nome = Console.ReadLine();
            Console.Write("Preço: ");
            double Preco = double.Parse(Console.ReadLine(), CultureInfo.InvariantCulture);
            

            Produto p = new Produto(Nome,Preco, Quantidade);

            Console.WriteLine();
            Console.WriteLine("Dados do produto: " + p);
            Console.WriteLine();
            Console.Write("Digite o número de produtos a ser adicionado ao estoque: ");
            int qte = int.Parse(Console.ReadLine());
            p.AdicionarProdutos(qte);
            Console.WriteLine();
            Console.WriteLine("Dados atualizados: " + p);
            Console.WriteLine();
            Console.Write("Digite o número de produtos a ser removido do estoque: ");
            qte = int.Parse(Console.ReadLine());
            p.RemoverProdutos(qte);
            Console.WriteLine();
            Console.WriteLine("Dados atualizados: " + p);
        }
    }
}

using System.Globalization;
namespace Course {
    class Produto {
        public string Nome;
        public double Preco;
        public int Quantidade;

        public Produto(string nome, double preco , int quantidade) {

            Nome = nome;
            Preco = preco;
            Quantidade = quantidade;

        }   
        public double ValorTotalEmEstoque() {
            return Preco * Quantidade;
        }
        public void AdicionarProdutos(int quantidade) {
            Quantidade += quantidade;
        }
        public void RemoverProdutos(int quantidade) {
            Quantidade -= quantidade;
        }
        public override string ToString() {
            return Nome
            + ", $ "
            + Preco.ToString("F2", CultureInfo.InvariantCulture)
            + ", "
            + Quantidade
            + " unidades, Total: $ "
            + ValorTotalEmEstoque().ToString("F2", CultureInfo.InvariantCulture);
        }
    }
}
```

Depois:

```csharp
using System;
using System.Globalization;
namespace Course {
    class Program {
        static void Main(string[] args) {
           
            

            Console.WriteLine("Entre os dados do produto:");
            Console.Write("Nome: ");
            string Nome = Console.ReadLine();
            Console.Write("Preço: ");
            double Preco = double.Parse(Console.ReadLine(), CultureInfo.InvariantCulture);
            

            Produto p = new Produto(Nome,Preco); /*instanciação somente com dois atributos, pois incluimos valor na Quantidade*/

						 Produto p2 = new Produto(); /*ele proibi a instanciação sem atributos, anão ser que criamos o metodo construtor sem nenhuma 
variavel vinculada nele, tem um exemplo abaixo*/

            Console.WriteLine();
            Console.WriteLine("Dados do produto: " + p);
            Console.WriteLine();
            Console.Write("Digite o número de produtos a ser adicionado ao estoque: ");
            int qte = int.Parse(Console.ReadLine());
            p.AdicionarProdutos(qte);
            Console.WriteLine();
            Console.WriteLine("Dados atualizados: " + p);
            Console.WriteLine();
            Console.Write("Digite o número de produtos a ser removido do estoque: ");
            qte = int.Parse(Console.ReadLine());
            p.RemoverProdutos(qte);
            Console.WriteLine();
            Console.WriteLine("Dados atualizados: " + p);
        }
    }
}

using System.Globalization;
namespace Course {
    class Produto {
        public string Nome;
        public double Preco;
        public int Quantidade;

        public Produto(string nome, double preco , int quantidade) {

            Nome = nome;
            Preco = preco;
            Quantidade = quantidade;

        }

        public Produto(string nome, double preco) {

                Nome = nome;
                Preco = preco;             /*esse é o metodo de sobrecarga*/
                Quantidade = 5;
        }

				public Produto(){
                            /*esse é o metodo foi criado somente para da exemplo na instanciação vazia no exemplo de cima*/  
        }

        public double ValorTotalEmEstoque() {
            return Preco * Quantidade;
        }
        public void AdicionarProdutos(int quantidade) {
            Quantidade += quantidade;
        }
        public void RemoverProdutos(int quantidade) {
            Quantidade -= quantidade;
        }
        public override string ToString() {
            return Nome
            + ", $ "
            + Preco.ToString("F2", CultureInfo.InvariantCulture)
            + ", "
            + Quantidade
            + " unidades, Total: $ "
            + ValorTotalEmEstoque().ToString("F2", CultureInfo.InvariantCulture);
        }
    }
}
```

# Sintaxe alternativa para iniciar valores

```csharp
using System;
using System.Globalization;
namespace Course {
    class Program {
        static void Main(string[] args) {

            Console.WriteLine("Entre os dados do produto:");
            Console.Write("Nome: ");
            string Nome = Console.ReadLine();
            Console.Write("Preço: ");
            double Preco = double.Parse(Console.ReadLine(), CultureInfo.InvariantCulture);

            Produto p = new Produto(Nome, Preco);

            Produto pp = new Produto {
                Nome="asfasdfa",      /*essa seria uma opção alternativa para atribuir valores*/
                Preco=80.0,
                Quantidade=10
            };

            Console.WriteLine();
            Console.WriteLine("Dados do produto: " + p);
            Console.WriteLine();
            Console.Write("Digite o número de produtos a ser adicionado ao estoque: ");
            int qte = int.Parse(Console.ReadLine());
            p.AdicionarProdutos(qte);
            Console.WriteLine();
            Console.WriteLine("Dados atualizados: " + p);
            Console.WriteLine();
            Console.Write("Digite o número de produtos a ser removido do estoque: ");
            qte = int.Parse(Console.ReadLine());
            p.RemoverProdutos(qte);
            Console.WriteLine();
            Console.WriteLine("Dados atualizados: " + p);
        }
    }
}
```

Claro! Vamos analisar o código passo a passo:

```csharp
using System.Globalization;
namespace Course {
  class Produto {
    public string Nome;
    public double Preco;
    public int Quantidade;

    public Produto() {
      Quantidade = 0; // Inicializa a quantidade como zero
    }

    public Produto(string nome, double preco) : this() { // Chama o construtor padrão
      Nome = nome; // Atribui o nome passado como parâmetro
      Preco = preco; // Atribui o preço passado como parâmetro
    }

    public Produto(string nome, double preco, int quantidade) : this(nome, preco) { // Chama o outro construtor
      Quantidade = quantidade; // Atribui a quantidade passada como parâmetro
    }
  }
}

```

A palavra-chave `this` em C# é usada para referenciar o objeto atual em que um método está sendo executado. Isso é especialmente útil quando um método tem um parâmetro com o mesmo nome de um atributo da classe.

Por exemplo, considere a classe `Produto` abaixo:

```
using System.Globalization;

namespace Course {
    class Produto {
        public string Nome;
        public double Preco;
        public int Quantidade;

        public Produto(string nome, double preco, int quantidade) {
            Nome = nome;
            Preco = preco;
            Quantidade = quantidade;
        }

        public double ValorTotalEmEstoque() {
            return Preco * Quantidade;
        }

        public void AdicionarProdutos(int quantidade) {
            Quantidade += quantidade;
        }

        public void RemoverProdutos(int quantidade) {
            Quantidade -= quantidade;
        }
    }
}

```

Se quisermos criar um construtor para a classe `Produto` que inicialize apenas os atributos `Nome` e `Preco`, podemos fazê-lo da seguinte forma:

```
public Produto(string nome, double preco) {
    Nome = nome;
    Preco = preco;
}

```

No entanto, se quisermos reutilizar este construtor para inicializar a quantidade com um valor padrão de 0, podemos fazer isso usando a palavra-chave `this`:

```
public Produto(string nome, double preco) : this(nome, preco, 0) {
}

```

Neste exemplo, o construtor sem parâmetros chama o construtor que recebe três parâmetros, passando `0` como terceiro argumento. Dessa forma, o atributo `Quantidade` é inicializado com o valor padrão de 0.
