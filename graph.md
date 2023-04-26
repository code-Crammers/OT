```matlab
%% lpp in graphical method
%% Max Z=3x1+4x2
%% s/t : 2x1+3x2<=6
%% 8x1+5x2<=8
%% 4x1+2x2<=9
%% x1,x2>=0
%% : is for all columns
clear all
clc
format short
x=0:0.01:10
A = [2 3; 8 5; 4 2]
B = [6;8;9]
n=size(A,1) %1 is for row
for i=1:n
    y(i,:)=(B(i)-A(i,1)*x)/A(i,2)
    y(find(y<0))=nan %% nan is not a number
    plot(x,y(i,:))
    hold on
    pt1(i,:)=[x(find(x==0)), y(i,find(x==0))]
    pt2(i,:)=[x(find(y(i,:)==0)), y(i,find(y(i,:)==0))]
end
int_p=[]
for i=1:n-1
    for j=i+1:n
        a=[A(i,:);A(j,:)]
        b=[B(i);B(j)]
        X=inv(a)*b
        if X>0
            int_p=[int_p X]
        end
    end
end
in=int_p'
ap=[pt1;pt2;in;0 0]
for i=1:n
    feas= A(i,1)*ap(:,1)+A(i,2)*ap(:,2)-B(i)
    ap(find(feas>0),:)=[]
end
C = [2 3]
z = ap*C'
[opt_val,index] = max(z)
opt_sol = ap(index,:)
```