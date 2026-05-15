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

        if (scanf("%d", &opcao) != 1) {
            printf("Entrada inválida! Digite um número.\n");
            while (getchar() != '\n'); // limpa buffer
            continue;
        }
        getchar(); // limpa buffer do Enter

        // CADASTRAR CLIENTE
        if (opcao == 1) {
            if (total < MAX) {
                clientes[total].id = total + 1;

                printf("Nome: ");
                fgets(clientes[total].nome, sizeof(clientes[total].nome), stdin);
                clientes[total].nome[strcspn(clientes[total].nome, "\n")] = '\0';

                printf("Telefone: ");
                fgets(clientes[total].telefone, sizeof(clientes[total].telefone), stdin);
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
            if (total == 0) {
                printf("Nenhum cliente cadastrado.\n");
            } else {
                int idBusca;
                int encontrado = 0;

                printf("Digite o ID do cliente: ");
                if (scanf("%d", &idBusca) != 1) {
                    printf("Entrada inválida!\n");
                    while (getchar() != '\n');
                    continue;
                }
                getchar();

                for (int i = 0; i < total; i++) {
                    if (clientes[i].id == idBusca) {
                        printf("Cliente encontrado:\n");
                        printf("ID: %d\n", clientes[i].id);
                        printf("Nome: %s\n", clientes[i].nome);
                        printf("Telefone: %s\n", clientes[i].telefone);
                        encontrado = 1;
                        break;
                    }
                }
                if (!encontrado) {
                    printf("Cliente com ID %d não encontrado.\n", idBusca);
                }
            }
        }

        // REMOVER CLIENTE
        else if (opcao == 4) {
            if (total == 0) {
                printf("Nenhum cliente cadastrado.\n");
            } else {
                int idRemove;
                int encontrado = 0;

                printf("Digite o ID do cliente a remover: ");
                if (scanf("%d", &idRemove) != 1) {
                    printf("Entrada inválida!\n");
                    while (getchar() != '\n');
                    continue;
                }
                getchar();

                for (int i = 0; i < total; i++) {
                    if (clientes[i].id == idRemove) {
                        // Desloca os elementos para "apagar" o cliente
                        for (int j = i; j < total - 1; j++) {
                            clientes[j] = clientes[j + 1];
                            clientes[j].id = j + 1; // atualiza IDs
                        }
                        total--;
                        encontrado = 1;
                        printf("Cliente removido com sucesso!\n");
                        break;
                    }
                }
                if (!encontrado) {
                    printf("Cliente com ID %d não encontrado.\n", idRemove);
                }
            }
        }

        // SAIR
        else if (opcao == 5) {
            printf("Encerrando o programa...\n");
        }

        // OPÇÃO INVÁLIDA
        else {
            printf("Opção inválida! Tente novamente.\n");
        }
    }

    return 0;
}

