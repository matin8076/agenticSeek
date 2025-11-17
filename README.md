sets
*i         /1*25/
v          /1*5/
IJ                  /1*6/
II(ij)  ãÌãæÚå ÇíÓÊÇå åÇí ÇäÊÞÇá ãæÞÊ ãæÌæÏ æíÔäåÇÏí/1*4/
ITs(ii)  ÇíÓÊÇå ÇäÊÞÇá ãæÞÊ ãæÌæÏ /1*2/
ITn(ii)  ÇíÓÊÇå ÇäÊÞÇá ãæÞÊ ÌÏíÏ/3*4/
JJ(ij) äÞÇØ ÊæáíÏ ÒÈÇáå  /5*6/
R                    /r1*r10/
V1(v)   ãÌãæÚå æÓÇíá äÞáíå /1*3/
V2(v)   ãÌãæÚå æÓÇíá ÊÑíáÑ åÇí äíãå Óäíä/4*5/
D   ãÌãæÚå ÆÝÚ ÒÈÇáå /1/
T  ãÌãæÚå ÑæÒ åÇí ÏÑ ÏæÑå ÈÑäÇãå ÑíÒí /t1*t6/
;
alias(i,j,e,ij,iii);
alias(T,tttt,L);
alias(j,jjj);

scalars
FRei The cost of moving ($) from the existing transfer station to the aggregation location i   /100000/
FMi  The fixed storage cost ($) of the existing transfer station i  /10000/
FSj                                                                 /4000/
FC                                                                   /1000/
Tjv                                                                 /10/
Dv1                                                                 /480/
W                                                                    /10/
Qv1                                                                  /5000  /
Qv2                                                                     /15000/
CC                                                                        /10/
TC                                                                         /2/
EC                                                                         /0.5/
FT                                                                         /1/
ET                                                                         /0.8/
P0                                                                        /0.5/
P                                                                          /0.95/
PP0                                                                       /0.8/
PP                                                                            /1/
ms   /100000/
NV /100/
mm   /10000000/
;
parameters
Sft(e)    /1 12, 2 23, 3 12, 4 22, 5 32, 6 12/
Spt(d)    /1 100/
Q(J)      /5 100, 6 103/
;

table  DD (i,j)

     1    2   3   4   5   6
 1   0   12  12  14  15  14
 2   0   12  12  14  15  14
 3   0   12  12  14  15  14
 4   0   12  12  14  15  14
 5   0   12  12  14  15  14
 6   0   12  12  14  15  14

 ;
 table  DDD(i,d)


    1
1  10
2  11
3  11
4  20
5  11
6  25



 ;
table  TT(i,j)

     1    2   3   4   5   6
 1   0   12  12  14  15  14
 2   0   12  12  14  15  14
 3   0   12  12  14  15  14
 4   0   12  12  14  15  14
 5   0   12  12  14  15  14
 6   0   12  12  14  15  14
 ;
table  S(i,j)

     1    2   3   4   5   6
 1   0   12  12  14  15  14
 2   0   12  12  14  15  14
 3   0   12  12  14  15  14
 4   0   12  12  14  15  14
 5   0   12  12  14  15  14
 6   0   12  12  14  15  14
 ;
FREE variable
z1
;
positive variable
alfa(i,d,v,t)
Tak(v,r,t,e)
ss(i)
sss(i,t)
z(e,i)
ww(i)
NT(i,d)
u(j,t)
u(i,t)
www(i,j,r,v,t)
aaaa
bbbb
cccc
dddd
eeee
ffff
gggg
hhhh
qqq(j,t)
qqqq(j,t)
;
binary variable
x(i,j,r,v,t)
y(j,v,r,t)
;

equations
obj
co1
co2
co3
co4
co5
co6
co7
co8
co9
co10
co11
co12
co13
co16
co17
co18
CO19
co20
co21
co22
co23
co24
co25
co26
co27
co28
co29
co30
co31
co32
co33
co34
co35
co36
co37
co38
co39
co40
co41
co42
co43
co44
co45
co46
co47

;
obj                                                         ..    z1=e=aaaa+bbbb+cccc+dddd+eeee+ffff-gggg+hhhh ;
co1                                                         ..    aaaa=e=sum((j,i,v(v1),r,t),CC*DD(i,j)*x(i,j,r,v,t));
co2                                                         ..    bbbb=e=sum((j,i,v(v1),r,t),(FC+EC)*DD(I,j)*(P0*x(i,j,r,v,t)+((P-P0)/QV1)*x(i,j,r,v,t)*qqq(j,t)));
co3                                                         ..    cccc=e=sum((i(II),D),TC*DDD(i,d)*NT(i,d));
co4                                                         ..    dddd=e=sum((i(II),d),(FT+ET)*DDD(i,d)*(PP0+PP-PP0));
co5                                                         ..    eeee=e=sum((e(ITs),i(II)),FRei*z(e,i));
co6                                                         ..    ffff=e=sum((i(ITs),e(its)),FMi*z(e,i))+sum(i(ITn),FMi*ww(i));
co7                                                         ..    gggg=e=sum(j(its),FSj*(1-sum(i(ii),Z(j,i))));
co8                                                         ..    hhhh=e=sum(i(II),FC*ss(i));
co9(j(JJ))                                                  ..    sum((v(v1),r,t),y(j,v,r,t))=g=1;
co10(j(JJ),T)                                               ..    sum((v(v1),r),y(j,v,r,t)) =l=1;
co11(j(JJ),t,r,v(v1))                                       ..    sum(i,x(i,j,r,v,t))=e=y(j,v,r,t);
co12(e,t,r,v(v1))                                           ..    sum(i,x(i,e,r,v,t))=e=sum(j,x(j,e,r,v,t));
co13(j(JJ),t)$( card(t)-1 )                                 ..    sum((v(v1),r),y(j,v,r,t))=l=sum((r,v(v1),tttt),y(j,v,r,tttt)$(ord(t)<ord(tttt)));
co16(i,j,v(v1),t,r)$(ord(i)<>ord(j))                        ..    x(i,j,r,v,t)=e=0;
co17(i,j,v(v1),t,r)$(ord(i)<>ord(j))                        ..    x(i,j,r,v,t)+x(j,i,r,v,t) =l=1;
co18(t,r,v(v1))                                             ..    sum(j,QQQ(j,t)*y(j,v,r,t))=l=Qv1;
co19(t,v(v1))                                               ..    sum ((i,j,r),tt (i,j)*x(j,i,r,v,t))+sum((j(JJ),r),Tjv*y(j,v,r,t))=l=Dv1;
co20(e(II),t,r,v(v1))                                       ..    sum(j(JJ),QQQ(j,t)*x(j,e,r,v,t))+sum((j(JJ),i(JJ)),QQQ(j,t)*x(j,i,r,v,t))=e= Tak(v,r,t,e);
co21(i(II),t)                                               ..    sum((v(v1),r),Tak(v,r,t,i))=e=sum((v(v2),d),alfa(i,d,v,t));
co22(i(ITs))                                                ..    sum((e(ITs)),z(e,i))=l=card(ITs)*z(i,i);
co23(i(ITn))                                                ..    sum(e(ITs),z(e,i))=l=card(ITs)*ww(i);
co24(e(ITs))                                                ..    sum(i(II),z(e,i))=l=1;
co25(e(ITs),i(ITn))                                         ..    z(e,i)=l=z(e,e)  ;
co26 (i(ITn),t)                                             ..    sss(i,t)=l=ww(i);
co27(i(ITs),t)                                              ..    sss(i,t)=l=z(i,i);
co28(i(II),T)                                               ..    sss(i,t)=l=ss(i)  ;
co29                                                        ..    sum(i(II),ss(i))=e= nv;
co30(i(II),t,r,v(v1))                                       ..    sum(j(JJ),x(j,i,r,v,t))=l=1;
co31(j(II),t,r,v(v1))                                       ..    sum(i(JJ),x(j,i,r,v,t))=l=1;
co32 (i(II),j(JJ),t,r,v(v1))                                ..    x(j,i,r,v,t)=l=sum(e(ITs),z(e,i));
co33 (i(ITn),j(JJ),t,r,v(v1))                               ..    x(j,i,r,v,t)=l=ww(i);
co34 (i(jj),j(JJ),t,r,v(v1))                                ..    x(j,i,r,v,t)=l=sum((jjj(IJ),iii(II)),x(j,i,r,v,t)) ;
co35 (i(II),t,d,v(v2))                                      ..    NT(i,d)=g= (alfa(i,d,v,t)/Qv2);
co36                                                        ..    sum((e(its),i(ii)), Sft(e)*z(e,i))+sum((e(itn),i(itn)),Sft(e)*ww(i))+sum(d,spt(d))=g=ms;
co37 (t,j(jj))                                              ..    QQQ(j,t)=e=q(j)*(ord(t)-qqqq(j,t));
*co38(j(jj),t,l)$(ord(l) < ord(t))                           ..    qqqq(j,t)=e=smax((r,v(v1)),y(j,v,r,l)*ord(l));
*co38(j(jj),t,l)$(CARD(l) = CARD(t)-1)                       ..    qqqq(j,t)=e=smax (sum((r,v(v1)),y(j,v,r,l)*ord(l)));
co38(j(JJ),t)                                               .. qqqq(j,t) =e= smax(l$(ord(l) < ord(t)), sum((r,v(v1)), y(j,v,r,l)*ord(l)));
*co39(j(jj),t,l)$(ord(l) < ord(t))                           ..    qqqq(j,t)=g=sum((r,v(v1)),y(j,v,r,l)*ord(l)) ;
co40(j(JJ),t)                                               ..    q(j)*(ord(t)-qqqq(j,t))=l=u(j,t)  ;
co41(j(JJ),t)                                               ..    u(j,t)=l=Qv1  ;
co42(i,j,t)$(ord(i)<>ord(j))                                ..    u(i,t)- u(j,t)+Qv1*(sum((v(v1),r),x(j,i,r,v,t)))+((Qv1-(q(j)*(ord(t)- qqqq(j,t)))-(q(j)*(ord(t)- qqqq(j,t)))))*sum((v(v1),r),x(j,i,r,v,t))=l=Qv1-(q(j)*(ord(t)- qqqq(j,t))) ;
co43(i,j,t,r,v)                                             ..    qqqq(j,t)*x(j,i,r,v,t)=e=www(i,j,r,v,t) ;
co44(i,j,t,r,v)                                             ..    www(i,j,r,v,t)=l= qqqq(j,t) ;
co45(i,j,t,r,v)                                             ..    www(i,j,r,v,t)=l= mm*x(j,i,r,v,t) ;
co46 (i,j,t,r,v)                                            ..    www(i,j,r,v,t)=g= qqqq(j,t)-((1-x(j,i,r,v,t))*mm) ;
co47(i,j,t,r,v)                                             ..    www(i,j,r,v,t)=g=0 ;
model zandagi/all/;
solve zandagi using mip minimizing z1;


