#include <stdio.h>
#include <stdlib.h>
#include <string.h>

// Define structures
typedef struct {
    int temperature;
    int humidity;
} Environment;

typedef struct {
    char name[50];
    int quantity;
} Crop;

typedef struct {
    Crop crops[5];
    int numCrops;
    Environment environment;
} Farm;

// Function prototypes
void displayMenu();
void plantCrop(Farm *farm);
void monitorEnvironment(Farm *farm);
void harvestCrops(Farm *farm);
void displayStatus(Farm *farm);

// Main function
int main() {
    Farm myFarm;
    myFarm.numCrops = 0;
    myFarm.environment.temperature = 25;
    myFarm.environment.humidity = 60;

    int choice;

    do {
        displayMenu();
        printf("Enter your choice: ");
        scanf("%d", &choice);

        switch (choice) {
            case 1:
                plantCrop(&myFarm);
                break;
            case 2:
                monitorEnvironment(&myFarm);
                break;
            case 3:
                harvestCrops(&myFarm);
                break;
            case 4:
                displayStatus(&myFarm);
                break;
            case 5:
                printf("Exiting the smart farm control system. Goodbye!\n");
                break;
            default:
                printf("Invalid choice. Please try again.\n");
        }
    } while (choice != 5);

    return 0;
}

// Function to display menu
void displayMenu() {
    printf("\nSmart Farm Control System\n");
    printf("1. Plant Crop\n");
    printf("2. Monitor Environment\n");
    printf("3. Harvest Crops\n");
    printf("4. Display Status\n");
    printf("5. Exit\n");
}

// Function to plant a crop
void plantCrop(Farm *farm) {
    if (farm->numCrops < 5) {
        Crop newCrop;
        printf("Enter crop name: ");
        scanf("%s", newCrop.name);

        printf("Enter quantity: ");
        scanf("%d", &newCrop.quantity);

        farm->crops[farm->numCrops] = newCrop;
        farm->numCrops++;

        printf("Crop planted successfully!\n");
    } else {
        printf("Cannot plant more crops. Maximum limit reached.\n");
    }
}

// Function to monitor environment
void monitorEnvironment(Farm *farm) {
    printf("\nCurrent Environment:\n");
    printf("Temperature: %d°C\n", farm->environment.temperature);
    printf("Humidity: %d%%\n", farm->environment.humidity);
}

// Function to harvest crops
void harvestCrops(Farm *farm) {
    if (farm->numCrops > 0) {
        printf("Harvesting crops...\n");
        // Simulate harvesting process
        for (int i = 0; i < farm->numCrops; i++) {
            printf("Harvesting %d units of %s\n", farm->crops[i].quantity, farm->crops[i].name);
        }

        printf("Crops harvested successfully!\n");
        farm->numCrops = 0; // Reset the number of crops after harvesting
    } else {
        printf("No crops available for harvest.\n");
    }
}

// Function to display farm status
void displayStatus(Farm *farm) {
    printf("\nFarm Status:\n");

    if (farm->numCrops > 0) {
        printf("Crops Planted:\n");
        for (int i = 0; i < farm->numCrops; i++) {
            printf("%s - Quantity: %d\n", farm->crops[i].name, farm->crops[i].quantity);
        }
    } else {
        printf("No crops planted.\n");
    }

    monitorEnvironment(farm);
}
