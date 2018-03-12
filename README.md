# test
```cpp
/*
* 2018 Xingzhenketuilishiti
* 3/5/2018
*****************************
* Multiple choice test with single possible answer
* Q1: The answer of this question is:
* A.A B.B C.C D.D
* Q2: The answer of Question Five is:
* A.C B.D C.A D.B
* Q3: A choice with an answer different from those of the rest three:
* A.Q3 B.Q6 C.Q2 D.Q4
* Q4: A choice with both quetsions having the same answer:
* A.Q1&Q5 B.Q2&Q7 C.Q1&Q9 D.Q6&Q10
* Q5: A choice with an answer thta is same with this question:
* A.Q8 B.Q4 C.Q9 D.Q7
* Q6: A choice with both answers same to that of Question Eight:
* A.Q2&Q4 B.Q1&Q6 C.Q3&Q10 D.Q5&Q9
* Q7: The least chosen answer among 10 questions:
* A.C B.B C.A D.D
* Q8: A Choice with an answer not adjacent to the answer of Question One:
* A.Q7 B.Q5 C.Q2 D.Q10
* Q9: The chance for Q1 and Q6 having the same answer
*     is the opposite to Q(X) and Q5 having the same answer, X is:
* A.Q6 B.Q10 C.Q2 D.Q9
* Q10: The difference between the highest frequency of an answer
*      and the lowest frequency of an answer
* A.3 B.2 C.4 D.1
*/
#include <iostream>
#include <iterator>
#include <algorithm>
using namespace std;

const int totalchoices(0x100000);
const int mask = 0x03;
const int q2map[4]={2, 3, 0, 1};
const int q7map[4]={2, 1, 0, 3};

int main()
{
  int ans[10];
  ostream_iterator<int> output(cout, " ");

  for (int idx=0; idx<totalchoices; idx++) {
    int temp = idx;
    int cnt[4]={0,0,0,0};
    int _ans;
    int maxd(0), mind(0);

    for (int j = 0; j < 10; j++) {
      int che = temp & mask;
      ans[j] = che;
      cnt[che]++;
      temp = temp >> 2;
    }
    maxd = max_element(cnt,cnt+4) - cnt;
    mind = min_element(cnt,cnt+4) - cnt;

    // Question 2:
    _ans = q2map[ans[4]];
    if (_ans != ans[1]) continue;

    // question 3
    _ans = 99;
    if ((ans[2] != ans[5]) && (ans[2] != ans[1]) && (ans[2] != ans[3]))
      _ans = 0;
    else if ((ans[5] != ans[2]) && (ans[5] != ans[1]) && (ans[5] != ans[3]))
      _ans = 1;
    else if ((ans[1] != ans[2]) && (ans[1] != ans[5]) && (ans[1] != ans[3]))
      _ans = 2;
    else if ((ans[3] != ans[2]) && (ans[3] != ans[5]) && (ans[3] != ans[1]))
      _ans = 3;
    if (_ans != ans[2]) continue;

    //Question 4:
    _ans = 99;
    if (ans[0] == ans[4]) _ans = 0;
    else if (ans[1] == ans[6]) _ans = 1;
    else if (ans[0] == ans[8]) _ans = 2;
    else if (ans[5] == ans[9]) _ans = 3;
    if (_ans != ans[3]) continue;

    // Question 5:
    _ans = 99;
    if (ans[7] == 0) _ans = 0;
    else if (ans[3] == 1) _ans = 1;
    else if (ans[8] == 2) _ans = 2;
    else if (ans[6] == 3) _ans = 3;
    if (_ans != ans[4]) continue;

    // Question 6:
    _ans = 99;
    if ((ans[1]==ans[3])&&(ans[1]==ans[7])) _ans = 0;
    else if ((ans[0]==ans[5])&&(ans[0]==ans[7])) _ans = 1;
    else if ((ans[2]==ans[9])&&(ans[2]==ans[7])) _ans = 2;
    else if ((ans[4]==ans[8])&&(ans[4]==ans[7])) _ans = 3;
    if (_ans != ans[5]) continue;

    // Question 7:
    _ans = q7map[mind];
    if (_ans != ans[6]) continue;

    // Question 8:
    _ans = 99;
    if (abs(ans[6] - ans[0]) > 1) _ans = 0;
    else if (abs(ans[4] - ans[0]) > 1) _ans = 1;
    else if (abs(ans[1] - ans[0]) > 1) _ans = 2;
    else if (abs(ans[9] - ans[0]) > 1) _ans = 3;
    if (_ans != ans[7]) continue;

    // Question 9:
    _ans = 99;
    bool _bval = (ans[0] == ans[5]);
    if (_bval !=(ans[5]==ans[4])) _ans = 0;
    else if (_bval !=(ans[9]==ans[4])) _ans = 1;
    else if (_bval !=(ans[1]==ans[4])) _ans = 2;
    else if (_bval !=(ans[8]==ans[4])) _ans = 3;
    if (_ans != ans[8]) continue;

    // Question 10:
    _ans = 99;
    if ((cnt[maxd]-cnt[mind])==3) _ans = 0;
    else if ((cnt[maxd]-cnt[mind])==2) _ans = 1;
    else if ((cnt[maxd]-cnt[mind])==4) _ans = 2;
    else if ((cnt[maxd]-cnt[mind])==1) _ans = 3;
    if (_ans != ans[9]) continue;

    copy(ans, ans+10, output);
    cout << endl;
   }
  return 0;
}
```
