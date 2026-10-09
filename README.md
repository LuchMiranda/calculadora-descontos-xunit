# Calculadora de Descontos (xUnit)

Atividade de **Garantia da Qualidade de Software** — solução .NET 10 para praticar testes unitários com xUnit.

## Estrutura

- `CalculadoraDescontos.App`: código de produção (`DescontoService`)
- `CalculadoraDescontos.Tests`: testes unitários com xUnit (`DescontoServiceTests`)

## Métodos testados

| Método | Retorno | Regra |
|---|---|---|
| `ObterCategoriaCliente(int totalCompras)` | `string` | BRONZE (< 5), PRATA (5 a 10), OURO (> 10) |
| `CalcularDescontoPorPercentual(int valorOriginal, int percentualDesconto)` | `int` | Valor final com o desconto aplicado |
| `EValidoParaCupom(int idade, bool primeiraCompra)` | `bool` | `true` se idade >= 18 **ou** primeira compra |

## [Fact] vs [Theory]

- **`[Fact]`**: teste único, **sem parâmetros**. Verifica sempre o mesmo cenário.
- **`[Theory]`**: teste **parametrizado**. Roda várias vezes, uma para cada `[InlineData(...)]`, com dados diferentes. Evita duplicar métodos de teste para cada cenário, e cada `InlineData` aparece como um teste individual no resultado.

Exemplo:

```csharp
[Theory]
[InlineData(2, "BRONZE")]
[InlineData(7, "PRATA")]
[InlineData(15, "OURO")]
public void ObterCategoriaCliente_DeveRetornarCategoriaEsperada(int totalCompras, string esperado)
{
    Assert.Equal(esperado, _service.ObterCategoriaCliente(totalCompras));
}
```

## Como executar os testes

Pré-requisito: [.NET SDK 10] instalado.

```bash
git clone https://github.com/LuchMiranda/calculadora-descontos-xunit.git
cd calculadora-descontos-xunit
dotnet test
```

## Licença

Distribuído sob a licença MIT. Veja o arquivo [LICENSE](LICENSE).
