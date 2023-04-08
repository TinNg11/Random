#include <iostream>
#include <fstream>
#include <algorithm>
#include <string>
#include <vector>
using namespace std;

string wordCount(const string& text) {
    string result = "";
    for (char c : text) {
        if (isalpha(c)) {
            result += c;
        }
        else {
            result += "";
        }
    }
    return result;
}


string removeNonAlphabeticChars(const string& text) {
    string result = "";
    for (char c : text) {
        if (isalpha(c)) {
            result += c;
        }
        else {
            result += " ";
        }
    }
    return result;
}

bool isPalindrome(string str) {
    int n = str.length();
    if (n <= 1) {
        return false;
    }

    for (int i = 0; i < n; i++) {
      if (!(isalpha(str[i]))) {
        str.erase(str.length()-1);
      }
    }

    n = str.length();
    for (int i = 0; i < n / 2; i++) {
        if (str[i] != str[n - i - 1]) {
            return false;
        }
    }
    return true;
}

int main() {

    string filename;
    cin >> filename;

    ifstream infile(filename);
    if (!infile) {
        cout << "File not found!" << endl;
        return 0;
    }

    int choice = -1;
    while (choice != 0) {
        cout << "--------------------------------------------------------------" << endl;
        cout << "Please make your choice:" << endl;
        cout << " 0 - Exit" << endl;
        cout << " 1 - Word count" << endl;
        cout << " 2 - Find the longest word that appears the last alphabetically" << endl;
        cout << " 3 - Replace all none alphabetical characters with whitespaces and output the new text on screen" << endl;
        cout << " 4 - Output all words in order of their lengths and alphabetically" << endl;
        cout << " 5 - Output all palindrome words" << endl;
        cout << "--------------------------------------------------------------" << endl;
        cin >> choice;

        if (choice == 0) {
            break;
        }

        else if (choice == 1) {
        int count = 0;
        char c;
        while (infile.get(c)) {
            if (isalpha(c)) {
                string word;
                word += c;
                while (infile.get(c) && isalpha(c)) {
                    word += c;
                }
                count++;
            }
        }
      
        infile.clear();
        infile.seekg(0); 
        cout << "The number of words in the text is " << count << endl;
        }

        else if (choice == 2) {
            string longestWord;
            string word;
            while (infile >> word) {
                word = wordCount(word);
                if (word.length() > longestWord.length() || (word.length() == longestWord.length() && word > longestWord)) {
                    longestWord = word;
                }
            }
            infile.clear(); 
            infile.seekg(0);
            cout << "The longest word that appears the last alphabetically is " << longestWord << endl;
        }

        else if (choice == 3) {
            string line;
            while (getline(infile, line)) {
                line = removeNonAlphabeticChars(line);
                cout << line << endl;
            }
            infile.clear(); 
            infile.seekg(0); 
        }

        else if (choice == 4) {
            vector<string> words;
            string word;
            while (infile >> word) {
            word.erase(remove_if(word.begin(), word.end(), [](char c) { return !isalpha(c); }), word.end());
            if (!word.empty()) {
                words.push_back(word);
            }
        }
            infile.clear(); 
            infile.seekg(0); 

            for (int i = 0; i < words.size(); i++) {
                for (int j = i + 1; j < words.size(); j++) {
                    if (words[i].length() > words[j].length() || (words[i].length() == words[j].length() && words[i] > words[j])) {
                        swap(words[i], words[j]);
                }
            }
        }
        ofstream outfile("sorted.txt");
        for (const auto& w : words) {
            outfile << w << endl;
        }
        outfile.close();

        }


        else if (choice == 5) {
            vector<string> palindromes;
            string word;
            while (infile >> word) {
                word.erase(remove_if(word.begin(), word.end(), [](char c) { return !isalnum(c); }), word.end());
                if (isPalindrome(word)) {
                  palindromes.push_back(word);
                }
            }

            if (palindromes.empty()) {
                break;
            } 
            
            else {
                for (int i = 0; i < palindromes.size(); i++) {
                    cout << palindromes[i] << endl;
                }
              }
            
            infile.clear(); 
            infile.seekg(0); 

            }
      

        else {
            cout << "Please only enter 0, 1, 2, 3, 4, or 5!" << endl;
        }
    }
        
    return 0;
}
