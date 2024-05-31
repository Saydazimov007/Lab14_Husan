# Lab14_Husan

#include <iostream>
#include <map>
#include <vector>
#include <algorithm>
#include <cctype>
#include <unordered_map>
#include <string>
#include <set>
#include <unordered_set>
#include <random>
#include <ctime>
#include <queue>
#include <stack>
using namespace std;

void outputMap(const map<int, double>& myMap) {
    for (const auto& pair : myMap) {
        cout << pair.first << ": " << pair.second << endl;
    }
}

void displayPairs(const unordered_map<string, int>& myMap) {
    cout << "Pairs in the map:\n";
    for (const auto& pair : myMap) {
        cout << pair.first << ": " << pair.second << endl;
    }
}

void show(const set<int>& s) {
    cout << "Elements in sorted order:";
    for (auto it = s.begin(); it != s.end(); ++it) {
        cout << " " << *it;
    }
    cout << endl;
}

void show(const unordered_set<int>& s) {
    cout << "Elements:";
    for (auto it = s.begin(); it != s.end(); ++it) {
        cout << " " << *it;
    }
    cout << endl;
}

void show(const multiset<int>& s) {
    cout << "Elements:";
    for (auto it = s.begin(); it != s.end(); ++it) {
        cout << " " << *it;
    }
    cout << endl;
}

bool isSymmetric(const vector<int>& nums) {
    int n = nums.size();
    if (n == 0) return false;
    vector<int> sorted_nums = nums;
    sort(sorted_nums.begin(), sorted_nums.end());
    for (int i = 0; i < n; ++i) {
        if (sorted_nums[i] % 10 != sorted_nums[n - 1 - i] % 10) {
            return false;
        }
    }
    return true;
}

void displayQueue(queue<int> q) {
    cout << "Elements in the queue:";
    while (!q.empty()) {
        cout << " " << q.front();
        q.pop();
    }
    cout << endl;
}

void clearQueue(queue<int>& q) {
    while (!q.empty()) {
        q.pop();
    }
}

int main() {
    cout << "Problem_1" << endl;
    map<int, int> m;
    m.insert(make_pair(1, 1));
    m.insert(make_pair(2, 4));
    m.insert(make_pair(3, 9));
    m.insert(make_pair(4, 16));
    m.insert(make_pair(5, 25));

    cout << "Elements in map:" << endl;
    for (auto it = m.begin(); it != m.end(); ++it) {
        cout << "[" << it->first << ", " << it->second << "]" << endl;
    }

    cout << "Squares:" << endl;
    for (auto it = m.begin(); it != m.end(); ++it) {
        cout << "Square of " << it->first << " is " << it->second << endl;
    }

    cout << "Problem_2" << endl;
    map<int, string> competitionResults;
    vector<pair<int, string>> students = {{74, "Mike"}, {76, "Elena"}, {93, "David"},
                                          {70, "George"}, {89, "Indira"}};
    sort(students.begin(), students.end(), greater<pair<int, string>>());
    for (size_t i = 0; i < students.size(); ++i) {
        competitionResults[i + 1] = students[i].second;
    }
    for (const auto& result : competitionResults) {
        cout << result.first << " place is " << result.second << ".\n";
    }

    cout << "Problem_3" << endl;
    map<char, int> alphabetPositions;
    for (char letter = 'A'; letter <= 'Z'; ++letter) {
        alphabetPositions[letter] = letter - 'A' + 1;
    }
    cout << "Enter an uppercase letter: ";
    char inputLetter;
    cin >> inputLetter;
    inputLetter = toupper(inputLetter);
    if (alphabetPositions.find(inputLetter) != alphabetPositions.end()) {
        cout << "Position of " << inputLetter << " is " <<
             alphabetPositions[inputLetter] << endl;
    } else {
        cout << "Invalid input. Please enter an uppercase letter." << endl;
    }

    cout << "Problem_4" << endl;
    map<int, double> myMap = {{4, 7.5}, {25, 6.01}, {-9, 3.2}, {12, 5.16}};
    cout << "Original map:\n";
    outputMap(myMap);
    myMap.insert(make_pair(3, 3.75));
    cout << "\nMap after inserting (3, 3.75):\n";
    outputMap(myMap);
    myMap.insert(make_pair(-10, 4.3));
    cout << "\nMap after inserting (-10, 4.3):\n";
    outputMap(myMap);

    auto it = myMap.find(12);
    if (it != myMap.end()) {
        cout << "\nThe value corresponding to key 12 is: " << it->second << endl;
    } else {
        cout << "\nKey 12 not found in the map.\n";
    }
    if (it != myMap.end()) {
        myMap.erase(it);
        cout << "\nMap after deleting pair with key 12:\n";
        outputMap(myMap);
    }

    it = myMap.find(-9);
    if (it != myMap.end()) {
        it->second = 4.44;
        cout << "\nMap after modifying value with key -9 to 4.44:\n";
        outputMap(myMap);
    }

    cout << "Problem_5" << endl;
    unordered_map<string, int> myMap1 = {{"Earth", 3}, {"Mercury", 1}, {"Venus", 2}};
    cout << "Initial map:\n";
    displayPairs(myMap1);

    myMap1.insert({"Mars", 4});
    cout << "\nMap after inserting ('Mars', 4):\n";
    displayPairs(myMap1);

    myMap1.emplace_hint(myMap1.end(), "Saturn", 6);
    myMap1.emplace_hint(myMap1.end(), "Neptune", 8);
    cout << "\nMap after inserting ('Saturn', 6) and ('Neptune', 8):\n";
    displayPairs(myMap1);

    cout << "\nSize of the map: " << myMap1.size() << endl;

    myMap1.erase("Venus");
    cout << "\nMap after deleting element with key 'Venus':\n";
    displayPairs(myMap1);

    cout << "Problem_6" << endl;
    multimap<int, int> myMultiMap = {{100, 3}, {150, 4}, {100, 90}};
    cout << "Number of keys equal to 100: " << myMultiMap.count(100) << endl;
    myMultiMap.insert({200, 32});
    myMultiMap.insert({100, -12});
    myMultiMap.insert({90, 45});
    auto it2 = myMultiMap.upper_bound(100);

    cout << "Keys and values at upper bound of key 100:\n";
    for (int i = 0; i < 2 && it2 != myMultiMap.end(); ++i, ++it2) {
        cout << "Key: " << it2->first << ", Value: " << it2->second << endl;
    }

    auto pairToDelete = myMultiMap.find(100);
    if (pairToDelete != myMultiMap.end()) {
        myMultiMap.erase(pairToDelete);
    }

    cout << "\nResulting map after deleting elements with key 100:\n";
    for (const auto& pair : myMultiMap) {
        cout << "Key: " << pair.first << ", Value: " << pair.second << endl;
    }

    cout << "Problem_7" << endl;
    int numUsers;
    cout << "Enter the number of users who want to register: ";
    cin >> numUsers;
    unordered_map<string, int> registeredUsers;
    for (int i = 0; i < numUsers; ++i) {
        string name;
        cin >> name;
        if (registeredUsers.find(name) == registeredUsers.end()) {
            registeredUsers[name] = 1;
            cout << "OK " << name << endl;
        } else {
            int count = registeredUsers[name]++;
            cout << name << count << endl;
        }
    }

    cout << "Problem_8" << endl;
    int n;
    cout << "Enter the number of values in the sequence: ";
    cin >> n;
    unordered_map<int, int> occurrences;
    for (int i = 0; i < n; ++i) {
        int num;
        cin >> num;
        occurrences[num]++;
    }
    bool isGood = true;
    for (const auto& pair : occurrences) {
        if (pair.second != pair.first) {
            isGood = false;
            break;
        }
    }
    if (isGood) {
        cout << "Good sequence.\n";
    } else {
        cout << "Bad sequence.\n";
    }

    cout << "Problem_9" << endl;
    set<int> s1 = {1, 2, 3};
    set<int> s2 = {3, 4, 5};
    set<int> resultSet;

    set_union(s1.begin(), s1.end(), s2.begin(), s2.end(),
              inserter(resultSet, resultSet.begin()));
    cout << "Union of s1 and s2:";
    for (const auto& elem : resultSet) {
        cout << " " << elem;
    }
    cout << endl;

    resultSet.clear();
    set_intersection(s1.begin(), s1.end(), s2.begin(), s2.end(),
                     inserter(resultSet, resultSet.begin()));
    cout << "Intersection of s1 and s2:";
    for (const auto& elem : resultSet) {
        cout << " " << elem;
    }
    cout << endl;

    resultSet.clear();
    set_difference(s1.begin(), s1.end(), s2.begin(), s2.end(),
                   inserter(resultSet, resultSet.begin()));
    cout << "Difference of s1 and s2:";
    for (const auto& elem : resultSet) {
        cout << " " << elem;
    }
    cout << endl;
    int maxValue = *mySet.rbegin();
    cout << "Maximum value in the set: " << maxValue << endl;

    cout << "Problem_11" << endl;
    unordered_set<int> mySet1 = {10, 20, 30};
    cout << "Initial set:";
    show(mySet1);

    cout << "\nEnter a value to insert: ";
    int value;
    cin >> value;
    mySet1.insert(value);
    cout << "Set after insertion:";
    show(mySet1);

    int sum = 0;
    for (const auto& elem : mySet1) {
        sum += elem;
    }
    cout << "\nSum of elements: " << sum << endl;

    cout << "Problem_12" << endl;
    multiset<int> myMultiSet = {10, 20, 10, 30, 20, 40};
    show(myMultiSet);

    myMultiSet.insert(30);
    cout << "\nMultiset after inserting 30:\n";
    show(myMultiSet);

    cout << "\nCount of 10 in the multiset: " << myMultiSet.count(10) << endl;

    myMultiSet.erase(20);
    cout << "\nMultiset after erasing all instances of 20:\n";
    show(myMultiSet);

    cout << "Problem_13" << endl;
    vector<int> v = {40, 30, 20, 10};
    if (isSymmetric(v)) {
        cout << "The vector is symmetric.\n";
    } else {
        cout << "The vector is not symmetric.\n";
    }

    cout << "Problem_14" << endl;
    int n1 = 5;
    cout << "Enter " << n1 << " integers: ";
    priority_queue<int, vector<int>, greater<int>> pq;
    for (int i = 0; i < n1; ++i) {
        int num;
        cin >> num;
        pq.push(num);
    }
    cout << "Priority queue elements in ascending order:";
    while (!pq.empty()) {
        cout << " " << pq.top();
        pq.pop();
    }
    cout << endl;

    cout << "Problem_15" << endl;
    queue<int> q;
    for (int i = 0; i < 5; ++i) {
        q.push(i + 1);
    }
    cout << "Queue before removing elements:\n";
    displayQueue(q);
    clearQueue(q);
    cout << "Queue after removing all elements:\n";
    displayQueue(q);

    cout << "Problem_16" << endl;
    stack<int> s;
    for (int i = 0; i < 5; ++i) {
        s.push(i + 1);
    }
    cout << "Stack before removing elements:\n";
    while (!s.empty()) {
        cout << s.top() << " ";
        s.pop();
    }
    cout << endl;
    cout << "Stack after removing all elements:\n";
    if (s.empty()) {
        cout << "Stack is empty.\n";
    }

    cout << "Problem_17" << endl;
    int n2 = 3;
    cout << "Enter " << n2 << " integers: ";
    vector<int> v1(n2);
    for (int i = 0; i < n2; ++i) {
        cin >> v1[i];
    }
    vector<int> v2(n2);
    for (int i = 0; i < n2; ++i) {
        cin >> v2[i];
    }
    vector<int> result(n2);
    transform(v1.begin(), v1.end(), v2.begin(), result.begin(), plus<int>());
    cout << "Sum of the two vectors:";
    for (int i = 0; i < n2; ++i) {
        cout << " " << result[i];
    }
    cout << endl;

    cout << "Problem 18\n";
    // 1. Push numbers into a stack
    stack<int> myStack;
    myStack.push(43);
    myStack.push(90);
    myStack.push(100);
    myStack.push(30);
    myStack.push(28);
    myStack.push(1);
    myStack.push(34);
    // 2. Print the size of stack
    cout << "Size of the stack: " << myStack.size() << endl;
    // 3. Display the value at top
    if (!myStack.empty()) {
        cout << "Value at top: " << myStack.top() << endl;
    } else {
        cout << "Stack is empty." << endl;
    }
    // 4. Delete required elements of stack and print the size
    while (!myStack.empty() && myStack.top() != 30) {
        myStack.pop();
    }
    cout << "Size of the stack after deleting required elements: " << myStack.size()
         << endl;
    return 0;
}

    cout << "Problem_10" << endl;
    set<int> mySet = {1, 2, 3};
    show(mySet);
    cout << "Enter a value to insert: ";
    int val;
    cin >> val;
    mySet.insert(val);
    show(mySet);
    
