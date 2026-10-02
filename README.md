# Mini-Banco-v.01
Apenas um simples banco 

E apenas um banco, cria o usuario deposita o valor de quanto deseja, consegue sacar com taxa de %2, o quanto de saldo contem na conta e o extrato da sua conta e a saida do programa

package projeto;
/* Projeto de Estudo
    livro think java
    variaveis e tipos primitivos
    entrada de dados com scannner
    metodos void e com retorno
    condicionais(if else if else, || &&)
    bolleanos e validação
    interações com for do while e while
    escopo de variaveis
   
    by: Hyoga
    versão 0.1*/
    import java.util.Scanner;
public class Minibanco {
    //CONSTANTES
    static final double LIMITE_SAQUE = 10000.00; //valor limite de saque
    static final double TAXA_SAQUE = 0.02; //taxa de saque 2%
   
   
    static void exibirExtrato(String[] extrato, int totalLinhas){
        System.out.println(" === EXTRATO === ");
        if( totalLinhas == 0){
            System.out.println("Nenhuma movimentação realizada");      
        }else {
            for(int i = 0; i < totalLinhas; i++){
                System.out.println(" " +extrato[i]);
            }
        }
        System.out.println(" ============================== ");
    }
 
    static int registrar(String[] extrato, int totalLinhas, String linhx){
        extrato[totalLinhas] = linhx;
        return totalLinhas + 1;
    }
 
    static double sacar(double saldo, double valor){
        return saldo - calcularTotalSaque(valor);
    }
    static double calcularTotalSaque(double valor){
        return valor + (valor * TAXA_SAQUE);
    }
 
    static boolean saldoSuficiente(double saldo, double valor){
        return valor <= LIMITE_SAQUE;
    }
 
    static boolean valorEhValido(double valor){
        return valor > 0;
    }
    static void exibirmenu(){
        System.out.println(" === BANCO === ");
        System.out.println(" 1 - DEPOSITAR ");
        System.out.println(" 2 - SACAR ");
        System.out.println(" 3 - CONSULTAR SALDO ");
        System.out.println(" 4 - VER ESTRATO ");
        System.out.println(" 5 - SAIR ");
        System.out.println("Digite uma das opções");
    }
 
    static double depositar (double saldo, double valor){
        return saldo + valor;
    }
    static void exibirSaldo(double saldo){
        System.out.printf("Saldo atual:R$  %.2f%n" , saldo);
    }
    public static void main(String[] args) {
    Scanner leia = new Scanner(System.in);
 
   
    double saldo = 0.0; //saldo inicial sempre zero
 
    int opcao = 1; //opcao do menu
 
    //Tela inicial
 
    String[] extrato = new String[50];
    int totalLinhas = 0;
 
    System.out.println("Diga seu nome");
    String nome = leia.nextLine();
 
    System.out.printf("Ola, %s Saldo inicial: %.2f%n",  nome, saldo);
   
    while (opcao != 0){
        exibirmenu();
        opcao = leia.nextInt();
       
        if(opcao == 1){
            System.out.println("Valor a Depositar");
            double valor = leia.nextDouble();
           
 
            if(!valorEhValido(valor)){
                System.out.println("Valor invalido deve ser maior que zero");
 
            }else{
                saldo = depositar(saldo, valor);
                System.out.printf("Deposito realizado com sucesso, Saldo atual: %.2f%n", saldo);
                totalLinhas = registrar(extrato, totalLinhas,
                String.format("Deposito: R$ %.2f" ,valor , saldo));
            }
        }
        else if(opcao == 2){
            System.out.println("Valor a Sacar ");
            double valorSaque = leia.nextDouble();
           
           
           
            if(!valorEhValido(valorSaque)){
            System.out.println("Valor invalido");
 
            }else if(valorSaque > LIMITE_SAQUE){
                System.out.println("Valor de saque acima do limite permitido");
            }
            else if(!saldoSuficiente(saldo, valorSaque)){
                System.out.println("Saldo insuficiente para saque");calcularTotalSaque(valorSaque);
            }else {
                double taxa = valorSaque * TAXA_SAQUE;
                saldo = sacar(saldo, valorSaque);
                System.out.printf("Saque realizado com sucesso, Taxa atual: %.2f%n", taxa);
                exibirSaldo(saldo);
                totalLinhas = registrar(extrato, totalLinhas,
                String.format("Saque: R$ %.2f%n, Saldo: %.2f%n", valorSaque, saldo));
            }
 
        }
        else if(opcao == 3){
            System.out.println("Consultar Saldo ");
            exibirSaldo(saldo);
        }
        else if(opcao == 4){
            System.out.println("Ver estrato ");
            exibirExtrato(extrato , totalLinhas);
        }
        else if(opcao == 5){
            System.out.println("Ate logo "+ nome);
            break;
        }
        else{
            System.out.println("Opção invalida");
        }
    }
 
    leia.close();
    }
}
 
 
