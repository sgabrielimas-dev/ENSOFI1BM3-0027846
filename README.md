# ENSOFI1BM3-0027846
#include <stdio.h>
#include <string.h>

#define MAX 100

// Estrutura do cliente
struct Cliente {
    int id;
    char nome[50];
    char telefone[20];
};

int main() {

    struct Cliente clientes[MAX];
    int total = 0;
    int opcao = 0;

    while (opcao != 5) {

        printf("\n===== SISTEMA DE CLIENTES =====\n");
        printf("1 - Cadastrar cliente\n");
        printf("2 - Listar clientes\n");
        printf("3 - Buscar cliente\n");
        printf("4 - Remover cliente\n");
        printf("5 - Sair\n");
        printf("Escolha uma opcao: ");

        scanf("%d", &opcao);
        getchar(); // limpa buffer

        // CADASTRAR CLIENTE
        if (opcao == 1) {

            if (total < MAX) {

                clientes[total].id = total + 1;

                printf("Nome: ");
                fgets(clientes[total].nome, 50, stdin);
                clientes[total].nome[strcspn(clientes[total].nome, "\n")] = '\0';

                printf("Telefone: ");
                fgets(clientes[total].telefone, 20, stdin);
                clientes[total].telefone[strcspn(clientes[total].telefone, "\n")] = '\0';

                total++;

                printf("Cliente cadastrado com sucesso!\n");

            } else {
                printf("Limite de clientes atingido!\n");
            }
        }

        // LISTAR CLIENTES
        else if (opcao == 2) {

            if (total == 0) {

                printf("Nenhum cliente cadastrado.\n");

            } else {

                printf("\n--- LISTA DE CLIENTES ---\n");

                for (int i = 0; i < total; i++) {

                    printf("ID: %d\n", clientes[i].id);
                    printf("Nome: %s\n", clientes[i].nome);
                    printf("Telefone: %s\n", clientes[i].telefone);
                    printf("-------------------------\n");
                }
            }
        }

        // BUSCAR CLIENTE
        else if (opcao == 3) {

            int idBusca;
            int encontrado = 0;

            printf("Digite o ID do cliente: ");
            scanf("%d", &idBusca);
            getchar();

            for (int i = 0; i < total; i++) {

                if (clientes[i].id == idBusca) {

                    printf("\n--- CLIENTE ENCONTRADO ---\n");
                    printf("ID: %d\n", clientes[i].id);
                    printf("Nome: %s\n", clientes[i].nome);
                    printf("Telefone: %s\n", clientes[i].telefone);

                    encontrado = 1;
                    break;
                }
            }

            if (!encontrado) {
                printf("Cliente nao encontrado.\n");
            }
        }

        // REMOVER CLIENTE
        else if (opcao == 4) {

            int idRemover;
            int encontrado = 0;

            printf("Digite o ID do cliente que deseja remover: ");
            scanf("%d", &idRemover);
            getchar();

            for (int i = 0; i < total; i++) {

                if (clientes[i].id == idRemover) {

                    encontrado = 1;

                    // desloca clientes para trás
                    for (int j = i; j < total - 1; j++) {
                        clientes[j] = clientes[j + 1];
                    }

                    total--;

                    // reorganiza IDs
                    for (int k = 0; k < total; k++) {
                        clientes[k].id = k + 1;
                    }

                    printf("Cliente removido com sucesso!\n");
                    break;
                }
            }

            if (!encontrado) {
                printf("Cliente nao encontrado.\n");
            }
        }

        // SAIR
        else if (opcao == 5) {
            printf("Encerrando sistema...\n");
        }

        // OPÇÃO INVÁLIDA
        else {
            printf("Opcao invalida!\n");
        }
    }

    return 0;
}
