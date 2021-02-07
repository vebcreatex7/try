#include <string>
#include <iostream>
#include <cstdio>
#include <cstring>
#include <cstdlib>
#include <vector>
#include <iomanip>
#include <iterator>
#include <utility>


struct position {
	int line;
	int column;
	friend std::ostream& operator << (std::ostream& os, const position& p) {
		os << "\n[" << p.line << " " << p.column << "]\n";
		return os;
	}
};

char CharToLower(char c) {
    return isupper(c) ? c - 'A' + 'a' : c; 
}

std::pair<std::vector<position>, std::string> GetVectorOfPos(const std::vector<std::string>& v) {
	std::vector<position> p;
	std::string text;
	position tmp;
	int l = 1, c = 0;
	int f = 0;
	std::string s;
	for (int i = 0; i < v.size(); i++) {
		s = v[i];
		if (s == "\0") {
			l++;
		} else {
			for (int j = 0; j < s.length(); j++) {
			if(s[j] == ' ' && j == s.length() - 1) {
				continue;
			}
			text += s[j];
			if (s[j] == ' ') {
				c++;
				tmp.line = l;
				tmp.column = c;
				p.push_back(tmp);
			}
			}
			c++;
				tmp.line = l;
			tmp.column = c;
			p.push_back(tmp);
			l++;
			c = 0;
			if (f == 0)
				text += ' ';
			f = 0;
		}
	}
	return std::make_pair(p, text);
}

std::string StringToLower(const std::string& s) {
	std::string tmp;
	for (int i = 0; i < s.length(); i++) {
		if (s[i] == ' ' &&  i == 0) {
			while (s[i + 1] == ' ') {
				i++;
			}
			i++;
		}
		tmp += CharToLower(s[i]);
		if (s[i] == ' ') {
			while (s[i + 1] == ' ') {
				i++;
			}
		}
	}
	while (tmp[tmp.length() - 1] == ' ') {
		tmp.pop_back();
	}
	
	return tmp;
}
int QuantityOfWords (std::string s) {
	int count = 0;
	for (int i = 0; i < s.length(); i++) {
		s[i] = CharToLower(s[i]);
		if (s[i] == ' ') {
			count++;
		}
	}
	count++;
	return count;
}

std::vector<int> prefix_function(const std::string& s) {
	int n = (int)s.length();
	std::vector<int> pi(n);
	for (int i = 1; i < n; ++i) {
		int j = pi[i - 1];
		while (j > 0 && s[i] != s[j]) {
			j = pi[j - 1];
		}
		if (s[i] == s[j]) {
			++j;
		}
		pi[i] = j;
	}
	return pi;
}


std::vector<int> KMP_v(const std::string& pattern, const std::string& text) {
	int m = pattern.length();
	int n = text.length();
	int shift = QuantityOfWords(pattern);
	std::vector<int> pi(m);
	pi = prefix_function(pattern);
	std::vector<int> ans;
	std::vector<position> p;
	int count = 0;
	int i = 0, j = 0;

	while (i < n) {
		if (text[i] == ' ') {
			count++;
		}
		if (pattern[j] == text[i]) {
			i++;
			j++;
		}

		if (j == m) {
			ans.push_back(count - shift + 2);
			j = pi[j - 1];
		} else if (i < n && pattern[j] !=text[i]) {
			if (j != 0) {
				j = pi[j - 1];
			} else {
				i++;
			}
		}

	}

	return ans;

}
 



int main(void) {
	std::ios::sync_with_stdio(false);
    std::cin.tie(nullptr);
	std::vector<std::string> patterns;
	std::vector<std::string> texts;
	std::vector<int> numberOfString;
	std::vector<int> ans;
	std::vector<position> p;
	std::string pattern;
	std::string text;
	std::string s;

	std::getline(std::cin, pattern);
	pattern = StringToLower(pattern);

	while (std::getline(std::cin, text)) {
		texts.push_back(StringToLower(text));
	}
	if (pattern[pattern.length() - 1] == ' ') {
		pattern.pop_back();
	}
	std::pair<std::vector<position>, std::string> pair = GetVectorOfPos(texts);
	ans = KMP_v(pattern, pair.second);
	for (auto a : ans) {
			std::cout << pair.first[a - 1].line << ", " << pair.first[a - 1].column << std::endl;
		}
}
