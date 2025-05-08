#include <iostream>
#include <cmath> // Para usar sqrt()
using namespace std;

// Função para ordenar um vetor (Bubble Sort)
void ordenar(float vetor[], int tamanho) {
    for (int i = 0; i < tamanho - 1; i++) {
        for (int j = 0; j < tamanho - 1 - i; j++) {
            if (vetor[j] > vetor[j + 1]) {
                float temp = vetor[j];
                vetor[j] = vetor[j + 1];
                vetor[j + 1] = temp;
            }
        }
    }
}

int main() {
    float notas[50];        // Vetor que armazena todas as notas
    int totalNotas = 0;     // Total de notas cadastradas
    int tentativas = 0;     // Contador de tentativas extras

    float n1, n2;

    // Entrada das duas primeiras notas
    cout << "Digite a primeira nota: ";
    cin >> n1;
    notas[totalNotas++] = n1;

    cout << "Digite a segunda nota: ";
    cin >> n2;
    notas[totalNotas++] = n2;

    // Calcula a média inicial
    float media = (n1 + n2) / 2;

    // Enquanto a média for menor que 6, solicitar nova tentativa
    while (media < 6.0) {
        float novaNota;
        cout << "\nMédia atual: " << media << ". Nota insuficiente.\n";
        cout << "Digite nova nota de recuperação: ";
        cin >> novaNota;

        notas[totalNotas++] = novaNota;  // Guarda a nota
        tentativas++;

        // Substitui a menor nota
        if (n1 < n2) {
            n1 = novaNota;
        } else {
            n2 = novaNota;
        }

        media = (n1 + n2) / 2; // Recalcula média
    }

    // Exibe resultado final
    cout << "\nMédia final atingida: " << media << endl;
    cout << "Tentativas extras realizadas: " << tentativas << endl;

    // Exibe todas as notas
    cout << "\nTodas as notas registradas: ";
    for (int i = 0; i < totalNotas; i++) {
        cout << notas[i] << " ";
    }

    // Cálculo da média geral
    float soma = 0;
    for (int i = 0; i < totalNotas; i++) {
        soma += notas[i];
    }
    float mediaGeral = soma / totalNotas;

    // Cálculo da mediana
    ordenar(notas, totalNotas);
    float mediana;
    if (totalNotas % 2 == 0) {
        int meio = totalNotas / 2;
        mediana = (notas[meio - 1] + notas[meio]) / 2;
    } else {
        mediana = notas[totalNotas / 2];
    }

    // Cálculo do desvio padrão (usando sqrt da cmath)
    float somaQuadrados = 0;
    for (int i = 0; i < totalNotas; i++) {
        float diferenca = notas[i] - mediaGeral;
        somaQuadrados += diferenca * diferenca;
    }
    float variancia = somaQuadrados / totalNotas;
    float desvioPadrao = sqrt(variancia);  // Aqui usamos a função sqrt da cmath

    // Exibe estatísticas finais
    cout << "\n\nEstatísticas:\n";
    cout << "Média geral das notas: " << mediaGeral << endl;
    cout << "Mediana das notas: " << mediana << endl;
    cout << "Desvio padrão: " << desvioPadrao << endl;

    return 0;
}
