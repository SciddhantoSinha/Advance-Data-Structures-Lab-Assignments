#include <iostream>
#include <fstream>
#include <string>
#include <cstdlib>
using namespace std;

struct IndexRecord {
    int key;
    int offset;
};

void createIndexFile() {
    ifstream inFile("data.txt", ios::in);
    ofstream outFile("index.txt", ios::out);
    int offset = 0;
    string line;
    while (getline(inFile, line)) {
        int key = atoi(line.c_str());
        IndexRecord record = { key, offset };
        outFile.write((char*)&record, sizeof(IndexRecord));
        offset = inFile.tellg();
    }
    inFile.close();
    outFile.close();
}

void searchIndexFile(int key) {
    ifstream inFile("index.txt", ios::in);
    IndexRecord record;
    while (inFile.read((char*)&record, sizeof(IndexRecord))) {
        if (record.key == key) {
            ifstream dataFile("data.txt", ios::in);
            dataFile.seekg(record.offset, ios::beg);
            string line;
            getline(dataFile, line);
            cout << "Found " << key << " at offset " << record.offset << " in data file: " << line << endl;
            dataFile.close();
            inFile.close();
            return;
        }
    }

    cout << "Key " << key << " not found in index file." << endl;
    inFile.close();
}

int main() {
    createIndexFile();

    int key;
    cout << "Enter key to search for: ";
    cin >> key;

    searchIndexFile(key);

    return 0;
}
