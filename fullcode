#include <iostream>
#include <set>
#include <unordered_map>
#include <vector>
#include <fstream>
#include <algorithm>
#include <sstream>
#include <string>
#include <unordered_set>

using namespace std;

// --- Задание 1: Однонаправленный список ---
template <typename T>
class SinglyLinkedList {
private:
    struct Node {
        T data;
        Node* next;
        Node(T val) : data(val), next(nullptr) {}
    };

    Node* head;

public:
    SinglyLinkedList() : head(nullptr) {}

    void add(T value) {
        Node* newNode = new Node(value);
        if (head == nullptr) {
            head = newNode;
        } else {
            Node* temp = head;
            while (temp->next != nullptr) {
                temp = temp->next;
            }
            temp->next = newNode;
        }
    }

    void insertAfterFirst(T E) {
        Node* temp = head;
        while (temp != nullptr && temp->next != nullptr) {
            if (temp->data == E) {
                Node* newNode = new Node(E);
                newNode->next = temp->next;
                temp->next = newNode;
                return;
            }
            temp = temp->next;
        }
    }

    void addFirst(T value) {
        Node* newNode = new Node(value);
        newNode->next = head;
        head = newNode;
    }

    void addLast(T value) {
        Node* newNode = new Node(value);
        if (head == nullptr) {
            head = newNode;
        } else {
            Node* temp = head;
            while (temp->next != nullptr) {
                temp = temp->next;
            }
            temp->next = newNode;
        }
    }

    void print() const {
        Node* temp = head;
        while (temp != nullptr) {
            cout << temp->data << " ";
            temp = temp->next;
        }
        cout << endl;
    }

    ~SinglyLinkedList() {
        while (head != nullptr) {
            Node* temp = head;
            head = head->next;
            delete temp;
        }
    }
};

// --- Задание 2: Двунаправленный список ---
template <typename T>
class DoublyLinkedList {
private:
    struct Node {
        T data;
        Node* next;
        Node* prev;
        Node(T val) : data(val), next(nullptr), prev(nullptr) {}
    };

    Node* head;
    Node* tail;

public:
    DoublyLinkedList() : head(nullptr), tail(nullptr) {}

    void addFirst(T value) {
        Node* newNode = new Node(value);
        if (head == nullptr) {
            head = tail = newNode;
        } else {
            newNode->next = head;
            head->prev = newNode;
            head = newNode;
        }
    }

    void addLast(T value) {
        Node* newNode = new Node(value);
        if (tail == nullptr) {
            head = tail = newNode;
        } else {
            newNode->prev = tail;
            tail->next = newNode;
            tail = newNode;
        }
    }

    void add(T value) {
        addLast(value);
    }

    void insertAfterFirst(T E) {
        Node* temp = head;
        while (temp != nullptr && temp->next != nullptr) {
            if (temp->data == E) {
                Node* newNode = new Node(E);
                newNode->next = temp->next;
                temp->next = newNode;
                if (newNode->next != nullptr) {
                    newNode->next->prev = newNode;
                }
                return;
            }
            temp = temp->next;
        }
    }

    void print() const {
        Node* temp = head;
        while (temp != nullptr) {
            cout << temp->data << " ";
            temp = temp->next;
        }
        cout << endl;
    }

    ~DoublyLinkedList() {
        while (head != nullptr) {
            Node* temp = head;
            head = head->next;
            delete temp;
        }
    }
};

// --- Класс UnorderedUniqueList ---
template <typename T>
class UnorderedUniqueList {
private:
    unordered_set<T> elements; // Используем unordered_set для обеспечения уникальности элементов

public:
    // Добавление элемента
    void add(T value) {
        elements.insert(value); // Повторяющиеся элементы не добавляются
    }

    // Удаление элемента
    void remove(T value) {
        elements.erase(value);
    }

    // Объединение двух коллекций
    UnorderedUniqueList Union(const UnorderedUniqueList& other) const {
        UnorderedUniqueList result;
        result.elements = elements;
        for (const auto& elem : other.elements) {
            result.add(elem);
        }
        return result;
    }

    // Исключение элементов другой коллекции
    UnorderedUniqueList Except(const UnorderedUniqueList& other) const {
        UnorderedUniqueList result;
        for (const auto& elem : elements) {
            if (!other.Contains(elem)) {
                result.add(elem);
            }
        }
        return result;
    }

    // Пересечение двух коллекций
    UnorderedUniqueList Intersect(const UnorderedUniqueList& other) const {
        UnorderedUniqueList result;
        for (const auto& elem : elements) {
            if (other.Contains(elem)) {
                result.add(elem);
            }
        }
        return result;
    }

    // Проверка наличия элемента
    bool Contains(T value) const {
        return elements.find(value) != elements.end();
    }

    // Вывод элементов
    void print() const {
        for (const auto& elem : elements) {
            cout << elem << " ";
        }
        cout << endl;
    }
};

// --- Задание 3: Перечень книг ---
void task3() {
    int n, m;
    cout << "Введите количество читателей и книг: ";
    cin >> n >> m;

    vector<string> books(m);
    cout << "Введите названия книг: ";
    for (int i = 0; i < m; ++i) {
        cin >> books[i];
    }

    vector<UnorderedUniqueList<string>> readers(n);
    cout << "Введите список прочитанных книг для каждого читателя:\n";
    for (int i = 0; i < n; ++i) {
        int k;
        cout << "Читатель " << i + 1 << ": сколько книг он прочитал? ";
        cin >> k;
        cout << "Введите названия прочитанных книг: ";
        for (int j = 0; j < k; ++j) {
            string book;
            cin >> book;
            readers[i].add(book);
        }
    }

    UnorderedUniqueList<string> allReaders = readers[0];
    UnorderedUniqueList<string> someReaders;
    UnorderedUniqueList<string> noReaders;

    for (int i = 1; i < n; ++i) {
        allReaders = allReaders.Intersect(readers[i]);
    }

    for (const auto& book : books) {
        bool readBySome = false;
        for (const auto& reader : readers) {
            if (reader.Contains(book)) {
                readBySome = true;
                someReaders.add(book);
                break;
            }
        }
        if (!readBySome) {
            noReaders.add(book);
        }
    }

    cout << "Книги, которые прочли все читатели: ";
    allReaders.print();

    cout << "Книги, которые прочли некоторые читатели: ";
    someReaders.print();

    cout << "Книги, которые никто не читал: ";
    noReaders.print();
}

// --- Задание 4: Символы из файла ---
void task4() {
    ifstream file("clovar.txt");
    if (!file.is_open()) {
        cout << "Не удалось открыть файл!" << endl;
        return;
    }

    vector<string> words;
    string word;

    // Чтение слов из файла
    while (file >> word) {
        words.push_back(word);
    }
    file.close();

    if (words.size() < 2) {
        cout << "Недостаточно слов для анализа!" << endl;
        return;
    }

    // Множество символов первого слова
    UnorderedUniqueList<char> firstWordChars;
    for (char c : words[0]) {
        firstWordChars.add(c);
    }

    // Множество общих символов всех остальных слов
    UnorderedUniqueList<char> commonChars;
    for (char c : words[1]) {
        commonChars.add(c);
    }

    for (size_t i = 2; i < words.size(); ++i) {
        UnorderedUniqueList<char> currentWordChars;
        for (char c : words[i]) {
            currentWordChars.add(c);
        }
        commonChars = commonChars.Intersect(currentWordChars);
    }

    // Исключение символов, которые есть в первом слове
    UnorderedUniqueList<char> result = commonChars.Except(firstWordChars);

    cout << "Символы, которых нет в первом слове, но присутствуют во всех остальных: ";
    result.print();
}

// --- Задание 5: Олимпиада ---
struct Participant {
    string lastName;
    string firstName;
    int grade;
    int score;
};

bool compareByScore(const Participant& a, const Participant& b) {
    return a.score > b.score;
}

void olympiad() {
    int N;
    cout << "Введите количество участников: ";
    cin >> N;

    if (N == 0) {
        cout << "Нет участников!" << endl;
        return;
    }

    vector<Participant> participants(N);
    cout << "Введите фамилию, имя, класс и балл каждого участника:" << endl;
    for (int i = 0; i < N; i++) {
        cin >> participants[i].lastName >> participants[i].firstName >> participants[i].grade >> participants[i].score;
    }

    // Сортируем участников по убыванию баллов
    sort(participants.begin(), participants.end(), compareByScore);

    // Диагностический вывод
    cout << "\nСортированный список участников:" << endl;
    for (const auto& p : participants) {
        cout << p.lastName << " " << p.firstName << " Класс: " << p.grade << " Балл: " << p.score << endl;
    }

    // Определяем топ-25%
    int top25Percent = (N + 3) / 4; // Округляем вверх
    int minScore = participants[top25Percent - 1].score;

    // Диагностический вывод для top25Percent
    cout << "\nЧисло участников: " << N << endl;
    cout << "Топ 25% участников: " << top25Percent << endl;
    cout << "Минимальный балл среди призеров: " << minScore << endl;

    // Уточняем, что все участники с баллом `minScore` входят в призеры
    while (top25Percent < N && participants[top25Percent].score == minScore) {
        top25Percent++;
    }

    // Подсчет числа призеров по классам
    vector<int> prizeCounts(5, 0); // Классы: 7, 8, 9, 10, 11
    cout << "\nУчастники, попавшие в призёры:" << endl;
    for (int i = 0; i < top25Percent; i++) {
        const auto& p = participants[i];
        if (p.grade >= 7 && p.grade <= 11) {
            prizeCounts[p.grade - 7]++;
            cout << p.lastName << " " << p.firstName << " Класс: " << p.grade << " Балл: " << p.score << endl;
        } else {
            cout << "Участник " << p.lastName << " " << p.firstName 
                 << " из класса " << p.grade << " не учитывается (вне диапазона классов)." << endl;
        }
    }

    // Вывод результата
    cout << "\nМинимальный балл призёра: " << minScore << endl;
    cout << "Число призёров по классам: ";
    for (int count : prizeCounts) {
        cout << count << " ";
    }
    cout << endl;
}

// --- Меню ---
int main() {
    int choice;

    while (true) {
        cout << "Выберите задачу (1-5) или 0 для выхода:\n";
        cout << "1. Задание 1: Однонаправленный список\n";
        cout << "2. Задание 2: Двунаправленный список\n";
        cout << "3. Задание 3: Неупорядоченное множество\n";
        cout << "4. Задание 4: Символы из файла\n";
        cout << "5. Задание 5: Олимпиада\n";
        cout << "0. Выход\n";
        cout << "Введите ваш выбор: ";
        cin >> choice;

        if (choice == 0) break;

        switch (choice) {
            case 1: {
                cout << "Задание 1 (Однонаправленный список):\n";
                SinglyLinkedList<int> list;
                list.add(1);
                list.add(2);
                list.add(3);
                list.add(4);
                list.print();
                list.insertAfterFirst(2);
                list.print();
                break;
            }
            case 2: {
                cout << "Задание 2 (Двунаправленный список):\n";
                DoublyLinkedList<int> list;
                list.addFirst(1);
                list.addLast(2);
                list.add(3);
                list.add(4);
                list.print();

                // Пользователь вводит новый элемент
                int newElement;
                cout << "Введите элемент для добавления в начало и в конец списка: ";
                cin >> newElement;
                list.addFirst(newElement);
                list.addLast(newElement);
                list.print();
                break;
            }
            case 3:
                 cout << "Задание 3 (Прочитанные книги):\n";
                 task3();
                 break;
            case 4:
                task4();
                break;
            case 5:
                setlocale(LC_ALL, "Russian");
                olympiad();
                return 0;
            default:
                cout << "Неверный выбор!" << endl;
        }
    }

    return 0;
}
