```matlab
clear all
clc
format short
a = [3 5; 3 4; 2 5]
b = [15;6;9]
ma=size(a,1)
id=eye(ma)
ind=[0 1 1]
index1=find(ind==1)
id(index1,:)=-id(index1,:)
A=[a , id]
m=size(A , 1)
n=size(A , 2)
ncm=nchoosek(n,m)
pair=nchoosek(1:n,m)
sol=[]
for i=1:ncm
    index=pair(i,:)
    A1=A(:,index)
    X=inv(A1)*b
    Y=zeros(n,1)
    Y(index,:)=X
    if Y>=0 & Y~=inf
        sol=[sol Y]
    end
end
sol
C=[2 3 0 0 0]
Z=C*sol
[maxv, maxi]=max(Z)
opt_sol=sol(:,maxi)
```