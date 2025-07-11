//    You are given:

//     a: A list of words (n total words)

//     b: A stream of characters (m total characters)

//     result: A list of boolean values indicating whether any word in a ends at that point in the stream b.

// Interpreting the logic:

// At each step i in b, you're supposed to:

//     Look at the stream so far: b[0..i]

//     Check if any of the words in a is a suffix of the current stream.

//     If yes, then result[i] = True; else, False.

// Sample 1:

// a = ["n", "arg", "nytr"]
// b = ['n','y','t','r','a','a','r','g']

// We check the stream at each step:

//     Step 0: 'n' → "n" is in a → True

//     Step 1: 'ny' → ends with "y" → not in a → False

//     Step 2: 'nyt' → ends with "t" → not in a → False

//     Step 3: 'nytr' → ends with "nytr" → in a → True

//     Step 4: 'nytra' → ends with "a" → not in a → False

//     Step 5: 'nytraa' → ends with "aa" or "a" → not in a → False

//     Step 6: 'nytraar' → ends with "ar" or "r" → not in a → False

//     Step 7: 'nytraarg' → ends with "arg" → in a → True

// ✅ This matches the result: [True, False, False, True, False, False, False, True]
// Sample 2:

// a = ["a", "aa"]
// b = ['a','a','a','b']

//     Step 0: 'a' → "a" in a → True

//     Step 1: 'aa' → "aa" in a → True

//     Step 2: 'aaa' → ends with "a", "aa" → both in a → True

//     Step 3: 'aaab' → ends with "b" → not in a → False

// ✅ Matches result: [True, True, True, False]
// ❓So the question is likely:

//     Given a list of words a and a stream of characters b, return a list result such that result[i] is True if any word in a is a suffix of the stream b[0..i]


// Brute force approach

#include <bits/stdc++.h>
using namespace std;

// Helper function to check if word is a suffix of stream
bool isSuffix(const vector<char>& stream, const string& word, int pos) {
    int wLen = word.size();
    if (wLen > pos + 1) return false; // can't be suffix if word is longer

    // Check last wLen characters
    for (int i = 0; i < wLen; ++i) {
        if (stream[pos - wLen + 1 + i] != word[i]) {
            return false;
        }
    }
    return true;
}

int main() {
    int n, m;
    cout << "Enter number of words (n): ";
    cin >> n;

    vector<string> a(n);
    cout << "Enter " << n << " words:\n";
    for (int i = 0; i < n; ++i) {
        cin >> a[i];
    }

    cout << "Enter number of stream characters (m): ";
    cin >> m;

    vector<char> b(m);
    cout << "Enter " << m << " characters:\n";
    for (int i = 0; i < m; ++i) {
        cin >> b[i];
    }

    vector<bool> result;

    for (int i = 0; i < m; ++i) {
        bool found = false;
        for (const string& word : a) {
            if (isSuffix(b, word, i)) {
                found = true;
                break;
            }
        }
        result.push_back(found);
    }

    cout << "Result: ";
    for (bool val : result) {
        cout << (val ? "True " : "False ");
    }
    cout << endl;

    return 0;
}


// Advanced Approach

#include <bits/stdc++.h>
using namespace std;

struct Node {
    array<int, 26> nxt;
    bool wordEnd = false;
    Node() { nxt.fill(-1); }
};

class StreamChecker {
public:
    StreamChecker(const vector<string>& words) {
        root = 0;
        trie.emplace_back();
        maxLen = 0;

        for (const string& w : words) {
            maxLen = max<int>(maxLen, w.size());
            int cur = root;
            for (int i = (int)w.size() - 1; i >= 0; --i) {
                int c = w[i] - 'a';
                if (trie[cur].nxt[c] == -1) {
                    trie[cur].nxt[c] = trie.size();
                    trie.emplace_back();
                }
                cur = trie[cur].nxt[c];
            }
            trie[cur].wordEnd = true;
        }
    }

    bool query(char ch) {
        buf.push_front(ch - 'a');
        if ((int)buf.size() > maxLen) buf.pop_back();

        int cur = root;
        for (int c : buf) {
            cur = trie[cur].nxt[c];
            if (cur == -1) return false;
            if (trie[cur].wordEnd) return true;
        }
        return false;
    }

private:
    vector<Node> trie;
    int root;
    int maxLen;
    deque<int> buf;
};

int main() {
    int n, m;
    cout << "Enter number of words (n): ";
    cin >> n;

    vector<string> a(n);
    cout << "Enter " << n << " words:\n";
    for (int i = 0; i < n; ++i) {
        cin >> a[i];
    }

    cout << "Enter number of stream characters (m): ";
    cin >> m;

    vector<char> b(m);
    cout << "Enter " << m << " characters:\n";
    for (int i = 0; i < m; ++i) {
        cin >> b[i];
    }

    StreamChecker sc(a);
    vector<bool> result;
    for (char ch : b) {
        result.push_back(sc.query(ch));
    }

    cout << "Result: ";
    for (bool v : result) {
        cout << (v ? "True " : "False ");
    }
    cout << endl;

    return 0;
}

