#include <iostream>

class Date {
private:
    int year;
    int month;
    int day;
    int hour;
    int minute;
    int second;
    bool isOurEra;

public:
    // Конструктор по умолчанию
    Date() : year(1960), month(1), day(1), hour(0), minute(0), second(0), isOurEra(true) {}

    // Конструктор с параметрами
    Date(int year, int month, int day, int hour, int minute, int second, bool isOurEra)
        : year(year), month(month), day(day), hour(hour), minute(minute), second(second), isOurEra(isOurEra) {}

    // Методы для получения нового объекта класса Date
    Date add(int years, int months, int days, int hours, int minutes, int seconds) const;
    Date subtract(int years, int months, int days, int hours, int minutes, int seconds) const;

    // Перегрузка операторов
    Date& operator=(const Date& other);
    friend std::ostream& operator<<(std::ostream& os, const Date& date);
    bool operator==(const Date& other) const;
    bool operator>(const Date& other) const;
    bool operator<(const Date& other) const;
    Date operator+(const Date& other) const;
    Date operator+=(const Date& other);
    Date operator-(const Date& other) const;
    Date operator-=(const Date& other);
};

// Вспомогательная функция для определения високосного года
bool isLeapYear(int year) {
    return (year % 4 == 0 && year % 100 != 0) || (year % 400 == 0);
}

// Реализация методов
Date Date::add(int years, int months, int days, int hours, int minutes, int seconds) const {
    int newYear = year + years;
    int newMonth = month + months;
    int newDay = day + days;
    int newHour = hour + hours;
    int newMinute = minute + minutes;
    int newSecond = second + seconds;

    // Обработка переполнений и коррекция даты
    while (newSecond >= 60) {
        newSecond -= 60;
        newMinute++;
    }

    while (newMinute >= 60) {
        newMinute -= 60;
        newHour++;
    }

    while (newHour >= 24) {
        newHour -= 24;
        newDay++;
    }

    while (newMonth > 12) {
        newMonth -= 12;
        newYear++;
    }

    // Обработка високосных годов и коррекция даты
    while (newDay > 28) {
        int daysInMonth = 31;

        if (newMonth == 4 || newMonth == 6 || newMonth == 9 || newMonth == 11) {
            daysInMonth = 30;
        }
        else if (newMonth == 2) {
            daysInMonth = isLeapYear(newYear) ? 29 : 28;
        }

        if (newDay > daysInMonth) {
            newDay -= daysInMonth;
            newMonth++;
        }
        else {
            break;
        }
    }

    return Date(newYear, newMonth, newDay, newHour, newMinute, newSecond, isOurEra);
}

Date Date::subtract(int years, int months, int days, int hours, int minutes, int seconds) const {
    int newYear = year - years;
    int newMonth = month - months;
    int newDay = day - days;
    int newHour = hour - hours;
    int newMinute = minute - minutes;
    int newSecond = second - seconds;

    while (newSecond < 0) {
        newSecond += 60;
        newMinute--;
    }

    while (newMinute < 0) {
        newMinute += 60;
        newHour--;
    }

    while (newHour < 0) {
        newHour += 24;
        newDay--;
    }

    while (newMonth <= 0) {
        newMonth += 12;
        newYear--;
    }

    // Обработка високосных годов и коррекция даты
    while (newDay <= 0) {
        int daysInPrevMonth = 31;

        if (newMonth == 2) {
            daysInPrevMonth = isLeapYear(newYear) ? 29 : 28;
        }
        else if (newMonth == 4 || newMonth == 6 || newMonth == 9 || newMonth == 11) {
            daysInPrevMonth = 30;
        }

        newDay += daysInPrevMonth;
        newMonth--;
    }

    return Date(newYear, newMonth, newDay, newHour, newMinute, newSecond, isOurEra);
}

Date& Date::operator=(const Date& other) {
    if (this != &other) {
        year = other.year;
        month = other.month;
        day = other.day;
        hour = other.hour;
        minute = other.minute;
        second = other.second;
        isOurEra = other.isOurEra;
    }
    return *this;
}

std::ostream& operator<<(std::ostream& os, const Date& date) {
    os << date.year << "-" << date.month << "-" << date.day << " " << date.hour << ":" << date.minute << ":" << date.second;
    if (!date.isOurEra) {
        os << " BC";
    }
    return os;
}

bool Date::operator==(const Date& other) const {
    return year == other.year && month == other.month && day == other.day &&
        hour == other.hour && minute == other.minute && second == other.second &&
        isOurEra == other.isOurEra;
}

bool Date::operator>(const Date& other) const {
    if (year > other.year) return true;
    if (year < other.year) return false;
    if (month > other.month) return true;
    if (month < other.month) return false;
    if (day > other.day) return true;
    if (day < other.day) return false;
    if (hour > other.hour) return true;
    if (hour < other.hour) return false;
    if (minute > other.minute) return true;
    if (minute < other.minute) return false;
    return second > other.second;
}

bool Date::operator<(const Date& other) const {
    return !(*this > other) && !(*this == other);
}

Date Date::operator+(const Date& other) const {
    return add(other.year, other.month, other.day, other.hour, other.minute, other.second);
}

Date Date::operator+=(const Date& other) {
    *this = *this + other;
    return *this;
}

Date Date::operator-(const Date& other) const {
    return subtract(other.year, other.month, other.day, other.hour, other.minute, other.second);
}

Date Date::operator-=(const Date& other) {
    *this = *this - other;
    return *this;
}

![aaa drawio (1)](https://github.com/Jennly666/OOP/assets/112813779/c39659b8-3b5f-4ccc-a410-f5b9c0aeeb95)

