# jogoBlackJack

package fundamentos;
import javax.swing.JOptionPane;
 

public class jogoBlackJack {

 

    public static void main(String[] args) {

        int[] minhascartas = new int[10];

        int[] baralho = new int[52];

        int dealer[] = new int[10];

        int fichas = 2000;

        int soma = 0;

        int atual;

        int retorno = 0;

        while (fichas > 0) {

            int aposta = apostar(fichas);

            baralho = montarbaralho(baralho);

            minhascartas = darCartas(minhascartas, baralho);

            mostrar(minhascartas);

            baralho = tirardobaralho(baralho, minhascartas);

            minhascartas = hit(minhascartas, baralho);

            for (int i = 0; i < minhascartas.length; i++) {

                System.out.println(minhascartas[i]);

            }

            atual = fichas;

            soma = somarcartas(retorno, minhascartas);

           

 

            boolean ganhou = true;

            if (soma > 21) {

                JOptionPane.showMessageDialog(null, "Voce perdeu  ");

                fichas = atual - aposta;

            } else {

 

                cartadealer(dealer, baralho);

                ganhou = resultado(ganhou, minhascartas, dealer);

                if (ganhou == true) {

                   

                    fichas = atual + (2 * aposta);

                } else {

                    fichas = atual - aposta;

                   

                }

            }

 

            JOptionPane.showMessageDialog(null, "Seu numero atual de fichas:   " + fichas);

 

        }

    }

 

    public static int[] montarbaralho(int[] x) {

        for (int i = 0; i < 52; i++) {

            if (i < 13) {

                x[i] = 13 - i;

            } else if (i < 26) {

                x[i] = 26 - i;

            } else if (i < 39) {

                x[i] = 39 - i;

            } else if (i < 52) {

                x[i] = 52 - i;

            }

        }

        return x;

    }

 

    public static int apostar(int x) {

        String aposta = JOptionPane.showInputDialog("Sua aposta (em n inteiros)");

        int valor = Integer.parseInt(aposta);

        while (x < valor) {

            JOptionPane.showMessageDialog(null, "Sua aposta esta maior do que seu numero de fichas!!  ");

            aposta = JOptionPane.showInputDialog("Voce tem " + x + " fichas, aposte novamente!!");

            valor = Integer.parseInt(aposta);

 

        }

 

        return valor;

    }

 

    public static int[] darCartas(int[] x, int[] baralho) {

        int indice1 = (int) (Math.random() * 53);

        int indice2 = (int) (Math.random() * 53);

        x[0] = baralho[indice1];

        x[1] = baralho[indice2];

        return x;

 

    }

 

    public static void mostrar(int[] x) {

        String carta1;

        String carta2;

        switch (x[0]) {

            case 1:

                carta1 = "A";

                break;

            case 11:

                carta1 = "J";

                break;

            case 12:

                carta1 = "Q";

                break;

            case 13:

                carta1 = "K";

                break;

            default:

                carta1 = "" + x[0];

                break;

        }

        switch (x[1]) {

            case 1:

                carta2 = "A";

                break;

            case 11:

                carta2 = "J";

                break;

            case 12:

                carta2 = "Q";

                break;

            case 13:

                carta2 = "K";

                break;

            default:

                carta2 = "" + x[1];

                break;

        }

        JOptionPane.showMessageDialog(null, "Suas cartas sao: \n" + "\n        | " + carta1 + "  |          |  " + carta2 + "  | \n");

    }

 

    public static int[] tirardobaralho(int[] b, int[] minhascartas) {

        if (minhascartas[0] == minhascartas[1]) {

            for (int i = 0; i < 26; i++) {

                if (minhascartas[0] == b[i]) {

                    b[i] = 0;

                }

            }

        }

        for (int j = 0; j < 13; j++) {

            if (minhascartas[0] == b[j]) {

                b[j] = 0;

            }

            if (minhascartas[1] == b[j]) {

                b[j] = 0;

            }

        }

        for (int k = 0; k < 13; k++) {

            if (minhascartas[0] == b[k]) {

                b[k] = 0;

            }

            if (minhascartas[1] == b[k]) {

                b[k] = 0;

            }

        }

        return b;

    }

 

    public static int[] hit(int[] x, int b[]) {

        switch (x[1]) {

                            case 11:

                                x[1] = 10;

                                break;

                            case 12:

                                x[1] = 10;

                                break;

                            case 13:

                                x[1] = 10;

                                break;

                          

 

                        }

         switch (x[0]) {

                            case 11:

                                x[0] = 10;

                                break;

                            case 12:

                                x[0] = 10;

                                break;

                            case 13:

                                x[0] = 10;

                                break;

                           

 

                        }

       

       

        int soma = x[0] + x[1];

        for (int i = 2; i < x.length; i++) {

 

            if (soma >= 21) {

                return x;

            } else {

                String escolha = JOptionPane.showInputDialog("Voce quer mais uma carta? (S/N)");

                String resposta = escolha.toLowerCase();

                if ("s".equals(resposta)) {

                    int indice = (int) (Math.random() * 53);

                    x[i] = b[indice];

                    String carta;

                    if (x[i] == 0) {

                        indice = (int) (Math.random() * 53);

                        x[i] = b[indice];

                       

                    }

 

                    switch (x[i]) {

                        case 1:

                            carta = "A";

                            break;

                        case 11:

                            carta = "J";

                            break;

                        case 12:

                            carta = "Q";

                            break;

                        case 13:

                            carta = "K";

                            break;

                        default:

                            carta = "" + b[indice];

                            ;

                            break;

 

                    }switch (x[i]) {

                            case 11:

                                x[i] = 10;

                                break;

                            case 12:

                                x[i] = 10;

                                break;

                            case 13:

                                x[i] = 10;

                                break;

                            default:

                                x[i] = b[indice];

                                break;

 

                        }

                        soma += x[i];

                    JOptionPane.showMessageDialog(null, "Sua carta:  " + carta + "\n" + " SOMA =   " + soma);

                } else {

                    return x;

                }

            }

        }

        return x;

    }

 

    public static int[] cartadealer(int[] d, int[] b) {

        int soma = 0;

 

        for (int i = 0; soma < 17; i++) {

            int indice = (int) (Math.random() * 53);

            d[i] = b[indice];

            String carta;

            if (d[i] == 0) {

                indice = (int) (Math.random() * 53);

                d[i] = b[indice];

 

            }

 

            switch (d[i]) {

                case 1:

                    carta = "A";

                    break;

                case 11:

                    carta = "J";

                    break;

                case 12:

                    carta = "Q";

                    break;

                case 13:

                    carta = "K";

                    break;

                default:

                    carta = "" + b[indice];

                    ;

                    break;

            }

 

            JOptionPane.showMessageDialog(null, "Carta do dealer : " + carta);

 

            switch (d[i]) {

                case 11:

                    d[i] = 10;

                    break;

                case 12:

                    d[i] = 10;

                    break;

                case 13:

                    d[i] = 10;

                    break;

                default:

                    d[i] = b[indice];

                    break;

            }

            soma += d[i];

            JOptionPane.showMessageDialog(null, "DEALER TOTAL: " + soma);

           

           

if(soma>17)           

return d;

        }

return d;

       

    }

 

    public static boolean resultado(boolean ganhou, int[] x, int[] y) {

        int somajogador = 0;

        int somadealer = 0;

       
 

        for (int i = 0; i < x.length; i++) {

            somadealer += y[i];

            somajogador += x[i];

            if (somadealer > 21) {

                JOptionPane.showMessageDialog(null, "Parabeens, você ganhou!!!");

                return true;

            } else if (x[i] == x[9]) {

                if (somajogador > somadealer) {

                    return true;

                } else {

                    return false;

                }

 

            }

 

        }

        return true;

    }

 

    public static int somarcartas(int x, int[] y) {

        int soma = 0;

        for (int i = 0; i < y.length; i++) {

            soma = soma + y[i];

            if (i == 9) {

                return soma;

            }

        }

 

        return x;

    }

}
