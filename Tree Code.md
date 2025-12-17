### Пример 11. Рабочий алгоритм расчета функции потерь при различных L по входным данным
``` Python
#!/usr/bin/python3
import sys
f=sys.stdin
F1={}
F2={}
int1 = 0
int2 = 0
min2 = 10000
max2 = -10000
for line in f:
res=line.split();
if res[0] in F1 : F1[''+res[0]]=F1[''+res[0]]+1
else : F1[''+res[0]]=1
int1=int1+1
if res[1] in F2 : F2[''+res[1]]=F2[''+res[1]]+1
else : F2[''+res[1]]=1
res0=int(res[0])
res1=int(res[1])
int2=int2+1
if max2 < res0 : max2 = res0
if max2 < res1 : max2 = res1
if min2 > res0: min2 = res0
if min2 > res1: min2 = res1
for k in F1.keys(): F1[''+k]=float(F1[''+k])/float(int1)
for k in F2.keys(): F2[''+k]=float(F2[''+k])/float(int2)
for k in xrange(min2,max2,1):
err1=0
err2=0
for l in xrange(min2,k,1):
if фstr(l) in F1:
err1=err1+F1[str(l)]
for l in xrange(k,max2,1):
if str(l) in F2:
err2=err2+F2[str(l)]
print str(k)+" "+str(err1+err2)
```

### Пример 12. Программа для обучения решающего дерева
```python
#!/usr/bin/python3
import sys
from sklearn import tree
import graphviz
f=sys.stdin
lines = f.read().split("\n")
XARR = []
YARR = []
for line in lines:
cols=line.split()
if(cols):
XARR.append([cols[0],cols[1],cols[2],cols[3]])
YARR.append(cols[4])
clf = tree.DecisionTreeClassifier()
clf = clf.fit(XARR, YARR)
dot_data = tree.export_graphviz(clf, out_file=None)
graph = graphviz.Source(dot_data)
graph.render("mytree")
```

### Пример 13. Программа для обучения и сохранения параметров обученной схемы во внешнем файле.
``` python
#!/usr/bin/python3
import sys48
from sklearn import tree
import graphviz
f=sys.stdin
lines = f.read().split("\n")
XARR = []
YARR = []
for line in lines:
cols=line.split()
if(cols):
XARR.append([cols[0],cols[1],cols[2],cols[3]])
YARR.append(cols[4])
clf = tree.DecisionTreeClassifier()
clf = clf.fit(XARR, YARR)
dot_data = tree.export_graphviz(clf, out_file=None)
graph = graphviz.Source(dot_data)
graph.render("mytree")
import pickle
s=pickle.dumps(clf)
ff=open("my_first_ai","wb")
ff.write(s)
ff.close()
```

### Пример 14. Программа для прогноза с использованием обученной решающей схемы.
``` python
#!/usr/bin/python3
import sys
from sklearn import tree
import graphviz
import pickle
ff=open("my_first_ai","rb")
s2=ff.read()
ff.close()
clf2=pickle.loads(s2)
f=sys.stdin
lines = f.read().split("\n")
for line in lines:
cols=line.split()
if(cols):
XARR=[cols[0],cols[1],cols[2],cols[3]]
YARR=cols[4]
r=clf2.predict([XARR])
print (str(XARR)+" "+str(YARR)+" "+str(r[0]))
```