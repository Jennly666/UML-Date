#include <iostream>
using namespace std;
#include <ctime>

int main() {
    setlocale(LC_ALL, "Russian");
    srand(time(0));
    int random_xi;
    int random_yi;
    int xi{ 0 };
    int yi{ 0 };
    int points{ 0 };
    int summ{ 0 };

    for (int i = 0; i < 5; ++i) {
        cout << "Введите координаты для выстрела " << i + 1 << " (xi и yi от -5 до 5): ";
        cin >> xi >> yi;
        random_xi = rand() % 11 + (-5);
        random_yi = rand() % 11 + (-5);
        xi += random_xi;
        yi += random_yi;

        double distance = sqrt(xi * xi + yi * yi);
        // [0, 1), [1, 2), [2, 3), [3, 4), [4, 5)
        points = 5 - static_cast<int>(distance);
        points = points & (~(points >> (sizeof(int) * 8 - 1))); //points = (points < 0) ? 0 : points;
        summ += points;
        cout << "Выстрел в координаты (" << xi << ", " << yi << ") заработал " << points << " баллов." << endl;
    }

    cout << "Сумма баллов: " << summ << endl;
    if (summ < 10) {
        cout << "Лузер!" << endl;
    }
    else {
        cout << "Победа!" << endl;
    }
}