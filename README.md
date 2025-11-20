#include <stdio.h>
#include <math.h>

double division(double, double);
double modulus(double, double);
void print_menu();

int main() {
    int choice;
    double first, second, result;

    do {
        print_menu();
        scanf("%d", &choice);

        if (choice == 8) {
            printf("\nExiting Calculator... Goodbye!\n");
            break;
        }

        if (choice < 1 || choice > 8) {
            fprintf(stderr, "\nInvalid Menu Choice. Try again!\n");
            continue;
        }

        if (choice == 7) { // Square Root needs only one number
            printf("\nEnter the number: ");
            scanf("%lf", &first);
            if (first < 0) {
                fprintf(stderr, "Square root of negative number is not real!\n");
                continue;
            }
            result = sqrt(first);
        } else {
            printf("\nEnter the first number: ");
            scanf("%lf", &first);
            printf("Enter the second number: ");
            scanf("%lf", &second);

            switch (choice) {
                case 1: result = first + second; break;
                case 2: result = first - second; break;
                case 3: result = first * second; break;
                case 4: result = division(first, second); break;
                case 5: result = modulus(first, second); break;
                case 6: result = pow(first, second); break;
                default: fprintf(stderr, "Unexpected error!\n"); continue;
            }
        }

        if (!isnan(result)) {
            printf("\nResult of operation is: %.2f\n", result);
        }

    } while (1);

    return 0;
}

double division(double a, double b) {
    if (b == 0) {
        fprintf(stderr, "Error: Division by zero!\n");
        return NAN;
    }
    return a / b;
}

double modulus(double a, double b) {
    if (b == 0) {
        fprintf(stderr, "Error: Modulus by zero!\n");
        return NAN;
    }
    return fmod(a, b); // works with doubles
}

void print_menu() {
    printf("\n\n===============================");
    printf("\n   Welcome to Smart Calculator");
    printf("\n===============================");
    printf("\n1. Add");
    printf("\n2. Subtract");
    printf("\n3. Multiply");
    printf("\n4. Divide");
    printf("\n5. Modulus");
    printf("\n6. Power");
    printf("\n7. Square Root");
    printf("\n8. Exit");
    printf("\nChoose an option (1-8): ");
}
