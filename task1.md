# Task 1 (12 points)

The function bool geegg(String s) returns:
- true, i.e. failure, if the string s contains three g characters or more,
- true, i.e. failure, if the string s contains two e characters or more,
- false, i.e. no failure, otherwise.

For instance, geegg("good eggs tomorrow") returns true, and geegg("no eggs today") returns false.
Apply ddmin() algorithm on the following inputs:
- a-debugging-exam
- as-easy-as-pie

Write down all the steps ddmin() would take to simplify these inputs.

### a-debugging-exam
1. let's give it a check first, we find there is three 'g' and two 'e'. Thus it returns true.
2. we start with n = 2. We split a-debugging-exam into two chunks: "a-debugg" and "ing-exam". We try to remove "a-debugg", then there is only 1 g and 1 e, geegg(a-debugg) = false. Thus we must keep chunk1.
3. Try to remove "ing-exam", there will be 1 e and 2 g left. Which also failed to preserver the failure. Thus none is removebale when n = 2. 
4. Let's have n=4 now. We have c1:a-de, c2:bugg, c3:ing-, c4:exam.
5. Removing c1. we have 3 g and 1 e. then geegg("bugging-exam") = true. Meaning ddmin is accepting this removal.
6. bugging-exam becoming the new input we are testing. We start over from n=2. c1:buggin, c2:g-exam. remove both c1 or c2 will result in a false. No asuccess removal. So we go to n=4
7. when n=4, c1=bug, c2=gin, c3=g-e, c4=xam. Removing c1. We have 1 g and 1 e, result in false. Then we removing c2, which is also result in false. Removing c3 is result in false, 2 g and 1 e. Finally we removing c4, this time we have 3 g and the result is true. Thus bugging-e become our new input.
8. Recursion on "bugging-e". Let's have n=2, c1=bugg, c2=ing-e. Removing any of the two will result in a false. 
9. Adjust to n=4, we have c1=bu, c2=gg, c3=in, c4=g-e. Remove c1 = remove "bu" = "gging-e", which will return true because of 3 g. 
10. Recursion on "gging-e". Start with n=2. c1=ggin, c2=g-e. Removing c1 or c2 will reusult in a false. 
11. So let's move on to n=4. c1=g, c2=g, c3=in, c4=g-e. remove c1 whill left 2g and 1e. remove c2 will left 2g and 1e. remove c3 will result in ture, which is success, which is "ggg-e".
12. keep recursion on "ggg-e", n=2, c1=gg, c2=g-e. both are not removable.
13. n=4 on "ggg-e", c1=g, c2=g, c3=g, c4=-e. remove c1, c2, or c3 will result in false. remove c4 will result in true. The input here will be "ggg".
14. recursion on "ggg", but it will fails no matter that. you cannot remove any letter to make it still has three 'g's. Thus 'ggg' is the 1-minimal we are looking for.

### as-easy-as-pie
1. The input is "as-easy-as-pie", now let do the initial check on the original input. It has two e and 0 g. The two e triggers geegg(as-easy-as-pie) = true.
2. Divide the input by n=2. c1=as-easy, c2=-as-pie. Both c1 and c2 are not removable. Thus we head to n=4.
3. now we have c1=as-, c2=eas, c3=y-a, c4=s-pie. By removing c1, we still have 2 e in the rest of input "easy-as-pie". 
4. Then we do recursion on easy-as-pie with n=2, c1=easy- and c2=as-pie. None of the two chuncks will result in true. So we move to n=4.
5. when n=4, c1=ea, c2=sy-, c3=as-, c4=pie. When you remove c1, it will result in false. when you remove c2, geegg("eaas-pie") = true. 
6. Another round of recursion with "eaas-pie". Start with n=2, we have c1=eaas, c2=-pie. None of them is removable.
7. Let's head to n=4, c1=ea, c2=as, c3=-p, c4=ie. remove c1 will result in false. Remove c2 will still result in true, so we delete c2.
8. A round of recursion with "ea-pie", when n=2, none of them is removeable. 
9. n=4 with "ea-pie", we have c1=e, c2=a, c3=-p, c4=ie. c2 is removable. Then we have "e-pie".
10. new recursion on "e-pie". when n=2, not removable. when n=4. We get a new input after the delete which will be "epie".
11. new recursion on "epie". when n=2, not removable. when n=4. We get a new input after the delete which will be "eie".
12. new recursion on "eie". when n=2, not removable. when n=4. We get a new input after the delete which will be "ee".
13. ee is not removable anymore. Thus we got the final answer "ee" as the 1-minimal.