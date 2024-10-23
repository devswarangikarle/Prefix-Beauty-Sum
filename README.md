# Prefix-Beauty-Sum

You are provided with N binary strings, each linked to a specific beauty value. You will receive Q queries, where each query consists of a string S. For every query, your task is to compute the sum of the beauty values of all binary strings that have S as a prefix. Due to potentially large sums, return the result modulo 10^9 + 7.

MOD = 10**9 + 7

class TrieNode:

    def __init__(self):
        self.children = {}
        self.beauty_sum = 0

class Trie:

    def __init__(self):
        self.root = TrieNode()
    
    def insert(self, string, beauty):
        node = self.root
        for char in string:
            if char not in node.children:
                node.children[char] = TrieNode()
            node = node.children[char]
            node.beauty_sum = (node.beauty_sum + beauty) % MOD
    
    def query(self, string):
        node = self.root
        for char in string:
            if char not in node.children:
                return 0
            node = node.children[char]
        return node.beauty_sum

def solve():

    N, Q = map(int, input().split())   
    trie = Trie()
    
    for _ in range(N):
        A, p = input().split()
        p = int(p)
        trie.insert(A, p)
    
    for _ in range(Q):
        S = input().strip()
        print(trie.query(S))
solve()
