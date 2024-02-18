TASK # 1

#include <iostream>
#include <vector>

using namespace std;

const int NUM_COWS = 5;  // Adjust this based on the actual number of cows

struct Cow {
    int id;
    vector<double> dailyYields;
};

// Function to record milk yields for a week (Task 1)
void recordYields(vector<Cow>& herd) {
    for (int day = 1; day <= 7; ++day) {
        cout << "Day " << day << ":\n";
        for (Cow& cow : herd) {
            double yield;
            cout << "Enter milk yield for cow " << cow.id << " (litres): ";
            cin >> yield;
            cow.dailyYields.push_back(yield);
        }
    }
}

int main() {
    vector<Cow> herd;

    // Initialize cow data with unique IDs
    for (int i = 1; i <= NUM_COWS; ++i) {
        Cow cow;
        cow.id = i;
        herd.push_back(cow);
    }

    // Task 1 - Record the yield
    recordYields(herd);

    // Output recorded data for verification
    cout << "\nRecorded Milk Yields:\n";
    for (const Cow& cow : herd) {
        cout << "Cow " << cow.id << ":\n";
        for (double yield : cow.dailyYields) {
            cout << yield << " ";
        }
        cout << "\n";
    }

    return 0;
}
--------------------------------------------------------------------------------------------------------------------------------

Task # 2

#include <iostream>
#include <iomanip>
#include <vector>

using namespace std;

const int NUM_COWS = 5;  // Adjust this based on the actual number of cows

struct Cow {
    int id;
    vector<double> dailyYields;
};

// Function to record milk yields for a week (Task 1)
void recordYields(vector<Cow>& herd) {
    for (int day = 1; day <= 7; ++day) {
        cout << "Day " << day << ":\n";
        for (Cow& cow : herd) {
            double yield;
            cout << "Enter milk yield for cow " << cow.id << " (litres): ";
            cin >> yield;
            cow.dailyYields.push_back(yield);
        }
    }
}

// Function to calculate statistics (Task 2)
void calculateStatistics(const vector<Cow>& herd) {
    double totalWeeklyVolume = 0.0;

    for (const Cow& cow : herd) {
        for (double yield : cow.dailyYields) {
            totalWeeklyVolume += yield;
        }
    }

    double averageYieldPerCow = totalWeeklyVolume / (herd.size() * 7);

    // Round to the nearest whole litre
    int roundedTotalVolume = static_cast<int>(totalWeeklyVolume + 0.5);
    int roundedAverageYield = static_cast<int>(averageYieldPerCow + 0.5);

    cout << fixed << setprecision(1);
    cout << "\nTotal weekly volume of milk for the herd: " << roundedTotalVolume << " litres\n";
    cout << "Average yield per cow in a week: " << roundedAverageYield << " litres\n";
}

int main() {
    vector<Cow> herd;

    // Initialize cow data with unique IDs
    for (int i = 1; i <= NUM_COWS; ++i) {
        Cow cow;
        cow.id = i;
        herd.push_back(cow);
    }

    // Task 1 - Record the yield
    recordYields(herd);

    // Task 2 - Calculate the statistics
    calculateStatistics(herd);

    // Output recorded data for verification
    cout << "\nRecorded Milk Yields:\n";
    for (const Cow& cow : herd) {
        cout << "Cow " << cow.id << ":\n";
        for (double yield : cow.dailyYields) {
            cout << yield << " ";
        }
        cout << "\n";
    }

    return 0;
}


task # 3

#include <iostream>
#include <iomanip>
#include <vector>
#include <numeric>

using namespace std;

const int NUM_COWS = 5;  // Adjust this based on the actual number of cows
const int MIN_LOW_VOLUME_DAYS = 4;
const double LOW_VOLUME_THRESHOLD = 12.0;

struct Cow {
    int id;
    vector<double> dailyYields;
};

// Function to record milk yields for a week (Task 1)
void recordYields(vector<Cow>& herd) {
    for (int day = 1; day <= 7; ++day) {
        cout << "Day " << day << ":\n";
        for (Cow& cow : herd) {
            double yield;
            cout << "Enter milk yield for cow " << cow.id << " (litres): ";
            cin >> yield;
            cow.dailyYields.push_back(yield);
        }
    }
}

// Function to calculate statistics (Task 2)
void calculateStatistics(const vector<Cow>& herd) {
    double totalWeeklyVolume = 0.0;

    for (const Cow& cow : herd) {
        for (double yield : cow.dailyYields) {
            totalWeeklyVolume += yield;
        }
    }

    double averageYieldPerCow = totalWeeklyVolume / (herd.size() * 7);

    // Round to the nearest whole litre
    int roundedTotalVolume = static_cast<int>(totalWeeklyVolume + 0.5);
    int roundedAverageYield = static_cast<int>(averageYieldPerCow + 0.5);

    cout << fixed << setprecision(1);
    cout << "\nTotal weekly volume of milk for the herd: " << roundedTotalVolume << " litres\n";
    cout << "Average yield per cow in a week: " << roundedAverageYield << " litres\n";

    // Task 3 - Identify the most productive cow and low-volume producers
    int mostProductiveCow = -1;
    double maxWeeklyYield = 0.0;

    cout << "\nCow(s) with less than 12 litres of milk for four or more days:\n";

    for (const Cow& cow : herd) {
        int lowVolumeDays = 0;
        for (double yield : cow.dailyYields) {
            if (yield < LOW_VOLUME_THRESHOLD) {
                lowVolumeDays++;
            }
        }

        if (lowVolumeDays >= MIN_LOW_VOLUME_DAYS) {
            cout << "Cow " << cow.id << "\n";
        }

        double weeklyYield = accumulate(cow.dailyYields.begin(), cow.dailyYields.end(), 0.0);
        if (weeklyYield > maxWeeklyYield) {
            maxWeeklyYield = weeklyYield;
            mostProductiveCow = cow.id;
        }
    }

    cout << "\nCow with the most milk production this week: Cow " << mostProductiveCow << "\n";
}

int main() {
    vector<Cow> herd;

    // Initialize cow data with unique IDs
    for (int i = 1; i <= NUM_COWS; ++i) {
        Cow cow;
        cow.id = i;
        herd.push_back(cow);
    }

    // Task 1 - Record the yield
    recordYields(herd);

    // Task 2 - Calculate the statistics
    calculateStatistics(herd);

    // Output recorded data for verification
    cout << "\nRecorded Milk Yields:\n";
    for (const Cow& cow : herd) {
        cout << "Cow " << cow.id << ":\n";
        for (double yield : cow.dailyYields) {
            cout << yield << " ";
        }
        cout << "\n";
    }

    return 0;
}
