```matlab
clc
clear all
format short
Cost=[11 20 7 8; 21 7 10 12; 8 12 18 9]
A=[50 40 70]
B=[30 25 35 40]
if sum(A)==sum(B)
    fprintf('Given Transportation problem is balanced\n')
else
    fprintf('Given Transportation problem is unbalanced\n')
    if sum(A)<sum(B)
        Cost (end+1,:)=zeros(1,size(B,2))
        A(end+1)=sum(B)-sum(A)
    elseif sum(B)<sum(A)
        Cost (:,end+1)=zeros(1,size(A,2))
        B(end+1)=sum(A)-sum(B)
    end
end
ICost=Cost
X=zeros(size(Cost))
[m,n]=size(Cost)
BC=m+n-1
for i=1:size(Cost,1)
    for j=1:size(Cost,2)
        hh=min(Cost(:))
        [Row_index,Col_index]=find(hh==Cost)
    x11=min(A(Row_index),B(Col_index))
    [Value,index]=max(x11)
    ii=Row_index(index)
    jj=Col_index(index)
    y11=min(A(ii),B(jj))
    X(ii,jj)=y11
    A(ii)=A(ii)-y11
    B(jj)=B(jj)-y11
    Cost(ii,jj)=inf
    end
end
fprintf('Initial BFS=\n')
TotalBFS=length(nonzeros(X))
if TotalBFS==BC
    fprintf('Initial BFS is Non-Degenerate\n')
else
    fprintf('Initial BFS is Degenerate\n')
end
InitialCost=sum(sum(ICost.*X))
fprintf('Initial BFS Cost is =%d\n ',InitialCost)
```