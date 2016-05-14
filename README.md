# CadastroC
#include <stdio.h>
#include <stdlib.h>
struct cadastros{
	int cod;
	char nome[50];
	char idade[50];
	char tempoServ[50];
	char quaDisc[50];
	char cadastro[50];
	int vazio;
};
struct cadastros vetor[50];
void cadastrar(int cod, int pos);
void consultar(void);
char relatorio(void);
//int verifica_pos(void);
int verifica_cod(int cod);
int verifica_pos(void);
void excluir(void);
int main(void) {
	int op = 0, posicao, codaux, retorno;
	while (op != 5) {
		printf("\n\n\t\t\t\tCADASTRO DE PROFESSORES\n\n\n");
		printf("MENU\n\n1 - Cadastrar\n2 - Pesquisar\n3 - Excluir\n4 - Relatorio\n5 - Sair\n\nOpcao: ");
		scanf("%d", &op);
		system("cls");
		switch (op) {
		case 1: {
			posicao = verifica_pos();
			if (posicao != -1) {
				printf("\nEntre com o codigo do professor (Somente numeros): \n");
				scanf("%d", &codaux); fflush(stdin);
				retorno = verifica_cod(codaux);
				if (retorno == 1)
					cadastrar(codaux, posicao);
				else
					printf("\nCodigo ja existente\n");
			}
			else
				printf("\nNao e possivel realizar mais cadastros!\n");
			break;
		}
		case 2: {
			consultar();
			break;
		}
		case 3: {
			excluir();
			break;
		}
		case 4: {
			relatorio(vetor);
		}
		case 5: {
			exit(0);
		}
		default:
			printf("Opcao Invalida");
			break;
		}
	}
	getchar();
	return 0;
}
void cadastrar(int cod, int pos){
	int i, contI, cont = 0;
	pos = verifica_pos();
	vetor[pos].cod = cod;
	fflush(stdin);
	printf("\nProdutora:\n");
	gets(vetor[pos].cadastro);
	printf("\nNome do professor: \n");
	gets(vetor[pos].nome);
	fflush(stdin);
	printf("\nIdade do professor: \n");
	gets(vetor[pos].idade);
	fflush(stdin);
	printf("\nTempo de servoço do professor: \n");
	gets(vetor[pos].tempoServ);
	fflush(stdin);
	printf("\nQuantidade de disciplinas do professor: \n");
	gets(vetor[pos].quaDisc);
	fflush(stdin);
	vetor[pos].vazio = 1;
	
	system("cls");
	printf("\nCadastro Realizado com Sucesso!\n\n");
	getchar();
}
void consultar(void){
	int cont = 0, cod;
	printf("\nEntre com o codigo\n");
	scanf("%d", &cod);
	system("cls");
	while (cont <= 50){
		if (vetor[cont].cod == cod){
			if (vetor[cont].vazio == 1){
				printf("\nNome do professor: \n%s\n", vetor[cont].nome);
				printf("\nIdade do professor: \n%s\n", vetor[cont].idade);
				printf("\nTempo de servoco do porfessor: \n%s\n", vetor[cont].tempoServ);
				printf("\nQuantidade de disciplinas ministradas: \n%s\n", vetor[cont].quaDisc);
				printf("\n");
				system("pause");
				system("cls");
				break;
			}
		}
		cont++;
		if (cont > 50)
			printf("\nCodigo nao encontrado\n");
	}
}
int verifica_pos(void){
	int cont = 0;
	while (cont <= 50){
		if (vetor[cont].vazio == 0)
			return(cont);
		cont++;
	}
	return(-1);
}
int verifica_cod(int cod){
	int cont = 0;
	while (cont <= 50){
		if (vetor[cont].cod == cod)
			return(0);
		cont++;
	}
	return(1);
}
 char relatorio(vetor){
	int contI, cont, contD, i, aux, auxD = 0;
	for (i = 0; i <= 50; i++) {

		aux = aux + vetor[i].quaDisc;
		auxD = aux / 50;
		if(vetor[i].idade >= 30 && vetor[i].idade <= 50) {
			contI++;
		}
		if (vetor[i].tempoServ >= 10) {
			cont++;
		}
		if (vetor[i].quaDisc > auxD) {
			contD++;
		}
	}
		printf("\n\n\nA quantidade de professores idade entre 30 e 50 anos e: %d\n", contI);
		printf("A quantidade de professores com mais de 10 anos de servico sao: %d", cont);
		printf("A media de disciplinas ministradas pelos professoes e: &d", auxD);
		printf("A quantidade de professores que ministram mias do que a media de disciplinas e: %d", contD);
		getchar();
}
void excluir(void){
	int cod, cont = 0;
	char resp;
	printf("\nEntre com o codigo do registro que deseja excluir\n");
	scanf("%d", &cod);
	while (cont <= 50){
		if (vetor[cont].cod == cod){
			if (vetor[cont].vazio == 1){
				printf("\nnome do professor: \n%s\n", vetor[cont].nome);
				printf("\nIdade o professor: \n%s\n", vetor[cont].idade);
				printf("\nTempo de servico do professor: \n%s\n", vetor[cont].tempoServ);
				printf("\nQuantidade de disciplina ministradas: \n%s\n", vetor[cont].quaDisc);
				getchar();
				printf("\nDeseja realmente exlucir? S/N:");
				scanf("%c", &resp);
				if ((resp == 'S') || (resp == 's')){
					vetor[cont].vazio = 0;
					printf("\nExclusao feita com sucesso\n");
					break;
				}
				else{
					if ((resp == 'N') || (resp == 'n')){
						printf("Exclusao cancelada!\n");
						break;
					}
				}
			}
		}
		cont++;
		if (cont > 50)
			printf("\nCodigo nao encontrado\n");
	}
	system("pause");
	system("cls");
}
