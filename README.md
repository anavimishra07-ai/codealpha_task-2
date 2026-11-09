# codealpha_task-2
#include <stdio.h>

#include <stdlib.h>

#define MAX 10

// Function prototypes
void inputMatrix(int matrix[MAX][MAX], int rows, int cols);
void displayMatrix(int matrix[MAX][MAX], int rows, int cols);
void addMatrices(int mat1[MAX][MAX], int mat2[MAX][MAX], int result[MAX][MAX], int rows, int cols);
void multiplyMatrices(int mat1[MAX][MAX], int mat2[MAX][MAX], int result[MAX][MAX], int r1, int c1, int c2);
void transposeMatrix(int matrix[MAX][MAX], int transpose[MAX][MAX], int rows, int cols);

int main() {
    int mat1[MAX][MAX], mat2[MAX][MAX], result[MAX][MAX], trans[MAX][MAX];
    int r1, c1, r2, c2;
    int choice;

    while (1) {
        printf("\n====================================");
        printf("\n          MATRIX OPERATIONS         ");
        printf("\n====================================");
        printf("\n1. Matrix Addition");
        printf("\n2. Matrix Multiplication");
        printf("\n3. Matrix Transpose");
        printf("\n4. Exit");
        printf("\nEnter your choice (1-4): ");
        scanf("%d", &choice);

        if (choice == 4) {
            printf("Exiting program. Goodbye!\n");
            break;
        }

        switch (choice) {
            case 1:
                printf("\nEnter rows and columns for matrices: ");
                scanf("%d %d", &r1, &c1);
                
                printf("\nEnter elements of Matrix A:\n");
                inputMatrix(mat1, r1, c1);
                printf("\nEnter elements of Matrix B:\n");
                inputMatrix(mat2, r1, c1);
                
                addMatrices(mat1, mat2, result, r1, c1);
                
                printf("\nResultant Matrix (A + B):\n");
                displayMatrix(result, r1, c1);
                break;

            case 2:
                printf("\nEnter rows and columns for Matrix A: ");
                scanf("%d %d", &r1, &c1);
                printf("Enter rows and columns for Matrix B: ");
                scanf("%d %d", &r2, &c2);

                if (c1 != r2) {
                    printf("\nError: Columns of Matrix A must equal rows of Matrix B for multiplication.\n");
                    break;
                }

                printf("\nEnter elements of Matrix A:\n");
                inputMatrix(mat1, r1, c1);
                printf("\nEnter elements of Matrix B:\n");
                inputMatrix(mat2, r2, c2);

                multiplyMatrices(mat1, mat2, result, r1, c1, c2);

                printf("\nResultant Matrix (A * B):\n");
                displayMatrix(result, r1, c2);
                break;

            case 3:
                printf("\nEnter rows and columns for the matrix: ");
                scanf("%d %d", &r1, &c1);

                printf("\nEnter matrix elements:\n");
                inputMatrix(mat1, r1, c1);

                transposeMatrix(mat1, trans, r1, c1);

                printf("\nOriginal Matrix:\n");
                displayMatrix(mat1, r1, c1);
                printf("\nTransposed Matrix:\n");
                displayMatrix(trans, c1, r1);
                break;

            default:
                printf("\nInvalid choice! Please select an option between 1 and 4.\n");
        }
    }
    return 0;
}

void inputMatrix(int matrix[MAX][MAX], int rows, int cols) {
    for (int i = 0; i < rows; i++) {
        for (int j = 0; j < cols; j++) {
            printf("Element [%d][%d]: ", i, j);
            scanf("%d", &matrix[i][j]);
        }
    }
}

void displayMatrix(int matrix[MAX][MAX], int rows, int cols) {
    for (int i = 0; i < rows; i++) {
        for (int j = 0; j < cols; j++) {
            printf("%d\t", matrix[i][j]);
        }
        printf("\n");
    }
}

void addMatrices(int mat1[MAX][MAX], int mat2[MAX][MAX], int result[MAX][MAX], int rows, int cols) {
    for (int i = 0; i < rows; i++) {
        for (int j = 0; j < cols; j++) {
            result[i][j] = mat1[i][j] + mat2[i][j];
        }
    }
}

void multiplyMatrices(int mat1[MAX][MAX], int mat2[MAX][MAX], int result[MAX][MAX], int r1, int c1, int c2) {
    for (int i = 0; i < r1; i++) {
        for (int j = 0; j < c2; j++) {
            result[i][j] = 0;
            for (int k = 0; k < c1; k++) {
                result[i][j] += mat1[i][k] * mat2[k][j];
            }
        }
    }
}

void transposeMatrix(int matrix[MAX][MAX], int transpose[MAX][MAX], int rows, int cols) {
    for (int i = 0; i < rows; i++) {
        for (int j = 0; j < cols; j++) {
            transpose[j][i] = matrix[i][j];
        }
    }
}
