# Proyecto_Integrador_2
Proyecto 
#include <stdlib.h>
#include <conio.h>
#include <iostream>
#include "Cliente.h"
#include "Cuenta.h"
#include "Deposito.h"
#include "Retiro.h"
#include "Transferencia.h"
using namespace std;

int main();

Cliente cl[2];
Cuenta cu[2];
Deposito de[10];
Retiro re[10];
Transferencia ta[10];

int main(){
	int op,i,j;
	
	
	//MENU PRINCIPAL QUE SE MUESTRA EN PANTALLA
    do{
    	system("clear"); //LIMPIA LA PANTALLA
    	cout << endl << "\t\t\t      SISTEMA BANCARIO" << endl << endl;
	    cout << " MENU PRINCIPAL" << endl << endl;
	    cout << " 1. Registrar Cliente" << endl;
	    cout << " 2. Mostrar Cliente" << endl;
		cout << " 3. Crear Cuenta" << endl;
		cout << " 4. Mostrar Cuentas" << endl;
	    cout << " 5. Depositos" << endl;
	    cout << " 6. Ver Depositos Realizados" << endl;
	    cout << " 7. Retiros" << endl;
	    cout << " 8. Ver Retiros Realizados" << endl;
	    cout << " 9. Transferencia" << endl;
	    cout << " 9. Ver Transferencias Realizadas" << endl;
	    cout << " 10. Cerrar Programa" << endl << endl;
	    cout << " Ingrese opcion: ";	
	    cin >> op;
	}while(op < 1 || op > 10); //REPITE EL PROCESO MIETRAS OP SEA MENOR QUE 1 O MAYOR QUE 10
	
	if(op == 1){
		for (i = 0; i < 2; i++) {
        	cl[i].registrarCliente();
    	}
    	main();
	}
	
	
	if(op == 2){
		for (i = 0; i < 2; i++) {
        	cl[i].mostrarClientes();
    	}
    	main();
	}
	
	if(op == 3){
		long dni;
		string nombres;
		int aux = 0;
		
		system("clear");
	    cout << endl << "\t\t\t      SISTEMA BANCARIO" << endl << endl;
		cout << " CREAR CUENTA" << endl << endl;
		cout << " Ingrese DNI del Cliente:     ";
		cin >> dni;
    	
    	for (i = 0; i < 2 && aux == 0; i++){
    		if (cl[i].verificarDNI(dni) == 1){
				nombres = cl[i].getNombres();
	    		cu[i].crearCuenta(nombres);
				aux = 1;
			}
		}
		
		if(aux == 0){
			cout << " DNI no encontrado. Presione una tecla para continuar..";
			getchar();
		}
			
    	
    	main();
	}
	
	if(op == 4){
		for (i = 0; i < 2; i++) {
        	cu[i].mostrarCuentas();
    	}
    	main();
	}
	
	if(op == 5){
		long nc;
		string nombres;
		int aux = 0;
		float deposito;
		
		system("clear");
	    cout << endl << "\t\t\t      SISTEMA BANCARIO" << endl << endl;
		cout << " DEPOSITOS" << endl << endl;
		cout << " Ingrese Numero de Cuenta: ";
		cin >> nc;
    	
    	for (i = 0; i < 2 && aux == 0; i++){
    		if (cu[i].verificarNCuenta(nc) == 1){
				nombres = cu[i].getCliente();
	    		de[i].Depositar(nombres,nc);
	    		deposito = cu[i].getSaldo()+de[i].getCantidad();
	    		cu[i].setSaldo(deposito);
				aux = 1;
			}
		}
		
		if(aux == 0){
			cout << " Numero de Cuenta no encontrado. Presione una tecla para continuar..";
			getchar();
		}
			
    	
    	main();
	}
	
	if(op == 6){
		for (i = 0; i < 2; i++) {
        	de[i].mostrarDepositos();
    	}
    	main();
	}
	
	if(op == 7){
		long nc;
		string nombres;
		int aux = 0;
		float retiro;
		
		system("clear");
	    cout << endl << "\t\t\t      SISTEMA BANCARIO" << endl << endl;
		cout << " RETIROS" << endl << endl;
		cout << " Ingrese Numero de Cuenta: ";
		cin >> nc;
    	
    	for (i = 0; i < 2 && aux == 0; i++){
    		if (cu[i].verificarNCuenta(nc) == 1){
				nombres = cu[i].getCliente();
	    		re[i].Retirar(nombres,nc);
	    		retiro = cu[i].getSaldo()-re[i].getCantidad();
	    		cu[i].setSaldo(retiro);
				aux = 1;
			}
		}
		
		if(aux == 0){
			cout << " Numero de Cuenta no encontrado. Presione una tecla para continuar..";
			getchar();
		}
			
    	
    	main();
	}
	
	if(op == 8){
		for (i = 0; i < 2; i++) {
        	re[i].mostrarRetiros();
    	}
    	main();
	}
	
	if(op == 9){
		long nc_origen, nc_destino;
		string nombres_o, nombres_d;
		int aux = 0, aux2 = 0;
		float incrementar, disminuir;
		
		system("clear");
	    cout << endl << "\t\t\t      SISTEMA BANCARIO" << endl << endl;
		cout << " TRANSFERENCIAS" << endl << endl;
		cout << " Ingrese Numero de Cuenta origen: ";
		cin >> nc_origen;
    	
    	cout << " Ingrese Numero de Cuenta destino: ";
		cin >> nc_destino;
    	
    	for (i = 0; i < 2 && aux == 0; i++){
    		if (cu[i].verificarNCuenta(nc_origen) == 1){
				for (j = 0; j < 2 && aux2 == 0; j++){
					
					if (cu[j].verificarNCuenta(nc_destino) == 1){
						nombres_o = cu[i].getCliente();
						nombres_d = cu[j].getCliente();
						ta[i].Transferir(nombres_o,nombres_d);
						
						//Resta saldo
						disminuir = cu[i].getSaldo()-ta[i].getCantidad();	
						cu[i].setSaldo(disminuir);
						
						//Incrementa saldo
						incrementar = cu[j].getSaldo()+ta[i].getCantidad();	
						cu[j].setSaldo(incrementar);
						aux2 = 1;
					}
				}
				aux = 1;
			}
		}
		
		if(aux == 0){
			cout << " Numero de Cuenta no encontrado. Presione una tecla para continuar..";
			getchar();
		}
			
    	
    	main();
	}
	
	if(op == 10){
		for (i = 0; i < 2; i++) {
        	ta[i].mostrarTransferencias();
    	}
    	main();
	}
	
	
	if(op == 11){
		exit(0);
	}
	
	
	system("pause");
	return 0;
}


