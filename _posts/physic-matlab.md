---
title:  物理实验matlab版
date: 2019-5-4 16:00:00
categories:
tags:
---
- 学号：2018040206 
- 姓名：李昊
```matlab
X=[1.95 3.90 10.60 13.55 9.25 2.95 ];    %输入数据
Y=[2.95 1.80 3.25 7.80 14.15 13.65 ];  %输入数据
X_1=[2.35 4.35 11.05 12.80 8.90 3.25];    %输入数据
Y_1=[3.45 2.35 3.70 7.80 13.60 13.00];  %输入数据
X_2=[3.25 4.90 10.00 11.60 8.45 3.65];    %输入数据
Y_2=[4.46 3.50 4.50 7.85 12.65 12.05];  %输入数据
X_4=[4.46, 5.50 8.55 9.85 7.65 4.65];    %输入数据
Y_4=[5.57 5.05 5.55 7.85 11.15 10.65];  %输入数据
X_8=[5.52 5.52 6.30 7.31 8.05, 6.95];    %输入数据
Y_8=[8.86 6.98 6.45 6.69 7.95, 9.20];  %输入数据

[x1,y1,r1,a]=circlefit(X,Y);
plot(X,Y,'r*');axis equal;hold on;

alpha=linspace(0,2*pi,100);
plot(x1+r1*cos(alpha),y1+r1*sin(alpha),'g-');
hold off
function [xc,yc,R,a]=circlefit(x,y)
% CIRCLEFIT 拟合函数
% 公式：x^2+y^2+a(1)*x+a(2)*y+a(3)=0

n=length(x);
xx=x.*x;
yy=y.*y;
xy=x.*y;

A=[sum(x) sum(y) n;sum(xy) sum(yy) sum(y);sum(xx) sum(xy) sum(x)];
B=[-sum(xx+yy);-sum(xx.*y+yy.*y);-sum(xx.*x+xy.*y)];
a=A\B;
xc = -0.5*a(1);
yc = -0.5*a(2);
R = sqrt(-(a(3)-xc^2-yc^2));
fprintf("circle:(%f, %f);  R= %f)", xc,yc, R)
end
```