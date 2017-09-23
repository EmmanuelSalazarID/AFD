# AFD
/*Salazar Canchola Ramón Emmanuel
150274
Expresion: aa(abc*)*
*/

package afd;

import java.util.Scanner;

public class AFD {
    int cont;
    char[] car;
    boolean aceptado;

    public static void main(String[] args) {
        AFD automata=new AFD();//se genera la instancia para AFD
        String cadena;//se declara la variable en el que se guardara la cadena a evaluar
        String resp;//almacena la respuesta para evaluar si volver a ejecutar el programa o no
        Scanner entra=new Scanner(System.in);//esta variable capturara de teclado
        do{
            System.out.print("Cadena: ");
            cadena=entra.next();//se toma la cadena
            automata.car=cadena.toCharArray();//se convierte en arreglo
            automata.inicio();//inicia la validacion de la cadena
            if(automata.aceptado){//si la cadena es aceptada lo imprime
                System.out.println("Aceptado");
            }
            else{
                System.out.println("No aceptado");//sino es aceptada imprime que no es aceptado
            }
            System.out.print("Validar otra Cadena?: ");
            resp=entra.next();//se captura la respuesta de si se ejecuta o no el programa de nuevo
        }while(resp.equals("si"));
        
    }
    
    public void inicio(){//aqui se inicializa en false la variable aceptado
        cont=0;
        aceptado=false;
        q0();//se llama a q0 que hara la primera validacion
    }
    
    public void q0(){
        System.out.println("q0");
        if(cont<car.length){
            if(car[cont]=='a'){//en q0 solo me evalua que el primer caracter sea una a de lo contrario la cadena no sera valida
                cont++;
                q1();//si es valida llama a q1
            }
            else qError();//qError me valida como erronea la cadena
        }
    }
    
    public void q1(){
        System.out.println("q1");
        if(cont<car.length){
            if(car[cont]=='a'){//en q1 valida que el segundo caracter sea otra a
                cont++;
                q2();//si es asi llama a q2
            }
            else qError();//sino llama a qError
        }
    }
    
    public void q2(){
        System.out.println("q2 Aceptacion");
        aceptado=true;//si la cadena termina en aa ya es valida por lo que q2 me da el estado valido
        if(cont<car.length){//si aun hay mas caracteres
            if(car[cont]=='a'){//q2 valida que el tercer caracter sea otra a
                cont++;
                q3();//si es asi llama a q3
            }
            else qError();//de lo contrario llama a qError
        }
    }
    
    public void q3(){
        System.out.println("q3");
        aceptado=false;//en q3 vuelve a darse un estado no valido ya que una tercera a tiene que ir acompañada de b
        if(cont<car.length){
            if(car[cont]=='b'){//evalua que sea b
                cont++;
                q4();//si es b llama a q4
            }
            else qError();//sino llama a qError
        }
    }
    public void q4(){
        System.out.println("q4 aceptacion");
        aceptado=true;//q4 es otro estado de aceptacion por lo cual, si la cadena acaba aqui sera aceptada
        if(cont<car.length){//si hay mas caracteres sigue evaluando
            if(car[cont]=='a'){//y valida que el caracter sea una a
                cont++;
                q3();//si es asi llama a q3 de tal forma que estaria repitiendo la subcadena ab
            }
            else if(car[cont]=='c'){//si no es a puede ser c
                cont++;
                q4();//si es se aplica recursividad con q4 infinitamente al ser c*
            }
            else qError();//si no es ninguna llama a qError
        }
    }
    
    public void qError(){
        System.out.println("Error.");//imprime el error
        aceptado=false;//da el valor de false para una cadena no valida
    }
    
}
