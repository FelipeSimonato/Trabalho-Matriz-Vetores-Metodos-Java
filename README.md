# Trabalho em Java para Estacionamento 

Imagine que você é dono de um estacionamento, você precisa cadastrar e excluir os veículos que chegam e saí, no fim do dia ver quanto faturou com seu estacionamento e para não ter confusão cada carro você cadastra com sua cor, modelo,e placa. E até mesmo ver quantas vagas ainda tem no seu estacionamento para ver se pode estacionar mais carros ou não.


import java.util.Scanner;

public class estaonamento {

    public static void inserirCarro(String[][] matriz, int linhas) {
        Scanner scanner = new Scanner(System.in);
        int linha;

        mostrarCarros(matriz, linhas);
        do {
            System.out.println("Informe onde você deseja inserir o carro com valores de 1 a " + linhas);
            linha = scanner.nextInt();
        } while (linha < 1 || linha > linhas);

        System.out.println("Insira o modelo do carro: ");
        matriz[linha - 1][0] = scanner.next();
        System.out.println("Insira a cor do carro: ");
        matriz[linha - 1][1] = scanner.next();
        System.out.println("Insira a placa do carro: ");
        matriz[linha - 1][2] = scanner.next();
        System.out.println("Insira o horário de chegada do carro: ");
        matriz[linha - 1][3] = scanner.next();
        System.out.println("Carro adicionado.");
    }

    public static void mostrarCarros(String[][] matriz, int linhas) {
        System.out.println("Modelo | Cor | Placa | Hora que chegou");
        for (int i = 0; i < linhas; i++) {
            System.out.print((i + 1) + " - ");
            for (int j = 0; j < 4; j++) {
                System.out.print(matriz[i][j] + " | ");
            }
            System.out.println();
        }
    }

    public static void calcularValor(String[][] matriz, int linhas) {
        float valorFinal = 0.0f;
        for (int i = 0; i < linhas; i++) {
            if (matriz[i][0] != null) {
                valorFinal += 5.0f;
            }
        }
        System.out.println("Valor total ganho do estacionamento: " + valorFinal + " R$");
    }

    public static void removerCarro(String[][] matriz, int linhas, String placa) {
        boolean encontrado = false;
        for (int i = 0; i < linhas; i++) {
            if (matriz[i][2] != null && matriz[i][2].equals(placa)) {
                encontrado = true;
                matriz[i][0] = null;
                matriz[i][1] = null;
                matriz[i][2] = null;
                matriz[i][3] = null;
            }
        }
        if (encontrado) {
            System.out.println("Carro removido.");
        } else {
            System.out.println("Carro não encontrado.");
        }
    }
    public static int calcularVagasDisponiveis(String[][] matriz, int linhas) {
        int vagasDisponiveis = 0;
        for (int i = 0; i < linhas; i++) {
            if (matriz[i][0] == null) {
                vagasDisponiveis++;
            }
        }
        return vagasDisponiveis;
    }

    public static void main(String[] args) {
        String[][] estacionamento;
        int capacidade, opcao;
        int colunas = 4;
        Scanner scanner = new Scanner(System.in);
        String placa;

        System.out.println("Informe a capacidade do estacionamento:");
        capacidade = scanner.nextInt();
        estacionamento = new String[capacidade][colunas];

        do {
            System.out.println("Escolha uma opção: \n 1 - Mostrar carros estacionados \n 2 - Inserir carro \n 3 - Calcular ganho do estacionamento \n 4 - Remover carro \n 5 - Mostrar vagas\n 0 - Sair");
            opcao = scanner.nextInt();
            switch (opcao) {
                case 0:
                    break;
                case 1:
                    mostrarCarros(estacionamento, capacidade);
                    break;
                case 2:
                    inserirCarro(estacionamento, capacidade);
                    break;
                case 3:
                    calcularValor(estacionamento, capacidade);
                    break;
                case 4:
                    System.out.println("Insira a placa do carro a ser removido:");
                    placa = scanner.next();
                    removerCarro(estacionamento, capacidade, placa);
                    break;
                case 5:
                    int vagasDisponiveis = calcularVagasDisponiveis(estacionamento, capacidade);
                    System.out.println("Quantidade de vagas disponíveis: " + vagasDisponiveis);
                    break;
                default:
                    System.out.println("Opção inválida!");
            }
        } while (opcao != 0);
    }
}
