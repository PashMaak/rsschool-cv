# Saloev Anushervon

![My Photo](https://image.tmdb.org/t/p/original/g4yz1mu1CV5irtLvXA5zXA1imBC.jpg)  
📍 Birmingham, England  
📧 saloev05@gmail.com  
📞 +992 988337676 / +44 07502550876  
💬 Discord: @pashmak.  
[GitHub](https://github.com/PashMaak) • [LinkedIn](https://www.linkedin.com/in/anushervon-saloev-4450452b4/) • [Codeforces](https://codeforces.com/profile/Pash_Mak)

---

## About Me
Since 10th grade, I have been passionate about competitive programming. For a year, I dedicated at least 8 hours a day to learning C/C++ in order to participate in prestigious olympiads. By the end of 11th grade, I won prizes at the Republican Olympiad in Tajikistan and at the [Eurasian Olympiad](https://neerc.ifmo.ru/school/archive/2023-2024/ru-olymp-team-russia-2023-standings.html).

I was admitted to the University of Birmingham, where I am currently studying.

I also enjoy playing various competitive games, such as CS2.

---

## Skills

- **Programming Languages:** C, C++, Python
- **Languages:** English (C2), Russian (Native), Tajik/Farsi (Native)

---

## Code Examples

# C++ [Problem](https://codeforces.com/contest/474/problem/F) • [Solution](https://codeforces.com/contest/474/submission/253479244)

```cpp
/*Pash_Mak*/
#include "bits/stdc++.h"
 
using ll = long long;
using str = std::string;
 
const int N = 1 << 17;
int n, tree[N << 1];
std::pair<int,int> b[N];
 
int get(int l, int r) {
    l += n, r += n;
    int ans = 0;
    while (l < r) {
        if (l & 1) ans = std::gcd(ans, tree[l++]);
        if (r & 1) ans = std::gcd(ans, tree[--r]);
 
        l >>= 1, r >>= 1;
    }
    return ans;
};
 
signed main() {
    std::ios_base::sync_with_stdio(false);
    std::cin.tie(nullptr);
 
    std::cin >> n;
 
    for (int i = 0; i < n; i++) {
        std::cin >> tree[i+n];
        b[i] = {tree[i+n], i};
    }
    for (int i = n-1; i > 0; i--) {
        tree[i] = std::gcd(tree[i << 1], tree[i << 1 | 1]);
    }
    std::sort(b, b+n);
 
    int q;
    std::cin >> q;
 
    while (q--) {
        int l, r;
        std::cin >> l >> r;
 
        int cur = get(l-1, r);
        int x = std::lower_bound(b, b+n, std::make_pair(cur, l-1)) - b;
        int y = std::upper_bound(b, b+n, std::make_pair(cur, r-1)) - b;
 
        std::cout << r-l+1 - y+x << '\n';
    }
 
    return 0;
}
```
# C [Problem](https://codeforces.com/gym/104344/problem/E) • [Solution](https://codeforces.com/gym/104344/submission/212676076)
```c
#include <stdio.h>
#include <math.h>
#include <limits.h>

int main() {
    int V;
    scanf("%d", &V);

    long long res = LLONG_MAX;

    for (int a = 1; a * a <= V; a++) {
        for (int b = 1; b * b <= V; b++) {
            if (V % (a * b) != 0) {
                continue;
            }
            int c = V / (a * b);
            res = fmin(res, 2 * (a * b + b * c + a * c));
        }
    }

    printf("%lld\n", res);

    return 0;
}
```

# Python Brief Statement: You are given data about dart hits from three players, and your task is to convert, analyze, and present this data to the user.

```py
# Importing Libraries
import csv
import matplotlib.pyplot as plt
import numpy as np
import math

# Structures(Class)
class Hits:
    def __init__(self, x, y):
        self.x = float(x)
        self.y = float(y)

# GLobal variable
file_name = 'dart_hits.csv'
Player = [[], [], []]
score_board = []

# Functions
def data_conversion(file_name):
    try:
        with open(file_name) as players_data:
            for data in csv.reader(players_data):
                if data[0] == '1':
                    Player[0].append(Hits(data[1], data[2]))
                elif data[0] == '2':
                    Player[1].append(Hits(data[1], data[2]))
                else:
                    Player[2].append(Hits(data[1], data[2]))
    except FileNotFoundError:
        print(f'Error File {'"'}{file_name}{'"'} not found!')
        quit()

def navigation_menu(option):
    if option == 'main':
        print('Choose an option:')
        print('1. Plot')
        print('2. Analyse Data')
        print('3. Exit')
    else:
        print('1. Scatter plot for Player 1')
        print('2. Scatter plot for Player 2')
        print('3. Scatter plot for Player 3')
        print('4. Scatter plot for all three players')
        print('5. Stacked bar chart showing score distribution for each player')
        print('6. Go back')

def plot_setup():
    ax = plt.subplot()

    # Sketching plot
    ax.spines['left'].set_position('zero')
    ax.spines['bottom'].set_position('zero')
    ax.spines['right'].set_position('zero')
    ax.spines['top'].set_position('zero')

    ax.spines['right'].set_color('black')
    ax.spines['left'].set_color('None')
    ax.spines['top'].set_color('black')
    ax.spines['bottom'].set_color('None')
    
    plt.xlim(-4, 4)
    plt.ylim(-4, 4)
    plt.xticks(range(-4, 5), color='blue')
    plt.yticks(range(-4, 5), color='blue')

    ax.set_xlabel('x', loc='right', labelpad=0, color='blue')
    ax.set_ylabel('y', loc='top', rotation='horizontal', labelpad=0, color='blue')

    ax.xaxis.set_label_coords(1.01, .43)
    ax.yaxis.set_label_coords(0.43, 0.98)

    ax.grid(False)
    plt.gca().set_aspect('equal')

def scatter_plot(player_number):
    ax = plt.subplot()

    # Defying which player to show
    if player_number == 4:
        ax.plot([hits.x for hits in Player[0]], [hits.y for hits in Player[0]], color='black', linestyle='None', marker='+', label='Player 1')
        ax.plot([hits.x for hits in Player[1]], [hits.y for hits in Player[1]], color='green', linestyle='None', marker='x', label='Player 2')
        ax.plot([hits.x for hits in Player[2]], [hits.y for hits in Player[2]], color='blue', linestyle='None', marker='o', label='Player 3')
        
        ax.set_title(f'Dart Hits for All Players', color='red')
        plt.legend(loc='upper left')
    else:
        ax.plot([hits.x for hits in Player[player_number - 1]], [hits.y for hits in Player[player_number - 1]], color='black', linestyle='None', marker='+')
        ax.set_title(f'Dart Hits for Player {player_number}', color='red')  
    
    # Displaying the hits by players
    plot_setup()
    plt.show()

def plot_navigation():
    navigation_menu('plot')
    option = input('Enter your choise: ')

    if option == '6':
        print('Returning to main menu...')
    else:
        if option < '5' and option > '0':
            scatter_plot(int(option))
        elif option == '5':
            scatter_bar()
        else:
            print('Invalid Input please try again!')
        plot_navigation()

def get_scores():
    for player_number in range(3):
        ten, five, one, zero, total_score = 0, 0, 0, 0, 0
        for coordinates in Player[player_number]:
            distance = (coordinates.x ** 2 + coordinates.y ** 2) ** 0.5

            if distance <= 1:
                ten += 1
                total_score += 10
            elif distance <= 2:
                five += 1
                total_score += 5
            elif distance <= 3:
                one += 1
                total_score += 1
            else:
                zero += 1

        score_board.append([ten, five, one, zero, total_score])

def scatter_bar():
    players = ['Player 1', 'Player 2', 'Player 3']

    scores_10 = [score_board[0][0], score_board[1][0], score_board[2][0]]
    scores_5 = [score_board[0][1], score_board[1][1], score_board[2][1]]
    scores_1 = [score_board[0][2], score_board[1][2], score_board[2][2]]
    scores_0 = [score_board[0][3], score_board[1][3], score_board[2][3]]

    x = np.arange(3)

    plt.bar(x, scores_10, color = 'red', label = '10 Points')
    plt.bar(x, scores_5, bottom = scores_10, color = 'blue', label = '5 Points')
    plt.bar(x, scores_1, bottom = np.array(scores_10) + np.array(scores_5), color = 'green', label = '1 Point')
    plt.bar(x, scores_0, bottom = np.array(scores_10) + np.array(scores_5) + np.array(scores_1), color = 'purple', label = '0 Points')

    plt.ylabel('Frequency')
    plt.title('Frequency of Hits')
    plt.xticks(x, players)

    plt.legend()
    plt.show()

def analysis_of_data():
    total_scores = [score_board[0][4], score_board[1][4], score_board[2][4]]
    total_scores.sort()

    # In case of uqual scores first to achive {first,second or third} score is awarded {first, second, third} place
    first_place, second_place, third_place, current_scores = '', '', '', [[0], [0], [0]]
    with open(file_name) as players_data:
        for data in csv.reader(players_data):
            distance = (float(data[1]) ** 2 + float(data[2]) ** 2) ** 0.5
            ind = int(data[0]) - 1

            if distance <= 1:
                current_scores[ind][0] += 10
            elif distance <= 2:
                current_scores[ind][0] += 5
            elif distance <= 3:
                current_scores[ind][0] += 1
            
            if not first_place and current_scores[ind][0] == total_scores[2]:
                first_place = f'Player {ind + 1}'
            elif not second_place and current_scores[ind][0] == total_scores[1]:
                second_place = f'Player {ind + 1}'
            elif not third_place and current_scores[ind][0] == total_scores[0]:
                third_place = f'Player {ind + 1}'

    # Calculation avg displacemnt by sum of x and y hits divided by their number
    player_stats = [[0, 0, 0], [0, 0, 0], [0, 0, 0]]
    for player_number in range(3):
        for hit in Player[player_number]:
            player_stats[player_number][0] += hit.x
            player_stats[player_number][1] += hit.y
            player_stats[player_number][2] += 1 # length
    
    for player_number in range(3):
        avg_x = player_stats[player_number][0] / player_stats[player_number][2]
        avg_y = player_stats[player_number][1] / player_stats[player_number][2]

        # Rounding up avg displacement
        avg_x = math.ceil(avg_x * 100) / 100
        avg_y = math.ceil(avg_y * 100) / 100
        print(f'Player {player_number + 1} scored {score_board[player_number][4]} and have an average displacement of ({avg_x}, {avg_y})')
    
    print(f'\nThird place belongs to {third_place}')
    print(f'Second place belongs to {second_place}')
    print(f'First place and the winner of the game is {first_place} 👑')

# Main body
data_conversion(file_name)
get_scores()

while True:
    navigation_menu('main')
    option = input('Enter your choice: ')

    if option == '1':
        plot_navigation()
    elif option == '2':
        print('')
        analysis_of_data()
    elif option == '3':
        print('Exiting...')
        break
    else:
        print('Invalid input please try again!')
```

---
## Working Experience
No working experience

---

## Education
Private School Hotam and "PV" (2012–2024)  
University of Birmingham (2024–current)

---

## English
Official TOEFL certificate with a score of 82 (2024)  
Official Duolingo English Test score of 125 (2024)  
Official Academic English Certificate – C2 level (2025)