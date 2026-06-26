Here are the **experiment names and MATLAB programs copyable** from your uploaded file. 

## Experiment 1: ASK Modulation and Demodulation

```matlab
clc;
clear all;
close all;

fm=input("enter the message frequency:");
fc=input("enter the carrier frequency:");

A=1;
t=0:0.001:1;

m=(A.*square(2*pi*fm*t)+A)/2;
c=sin(2*pi*fc*t);
s=m.*c;

subplot(5,1,1);
plot(t,m);
title('MESSAGE SIGNAL');
xlabel('t---->');
ylabel('m(t)');
grid on;

subplot(5,1,2);
plot(t,c);
title('CARRIER SIGNAL');
xlabel('t---->');
ylabel('c(t)');
grid on;

subplot(5,1,3);
plot(t,s);
title('ASK SIGNAL');
xlabel('t---->');
ylabel('s(t)');
grid on;

y_dem = c.*s;

for i=0:1000
    if(y_dem(i+1)>0)
        X(i+1)=1;
    else
        X(i+1)=0;
    end
end

subplot(5,1,4);
plot(t,X);

subplot(5,1,5);
plot(t,X);
title('ASK Demodulated signal');
xlabel('t--->');
ylabel('b(n)');
```

## Experiment 2: FSK Modulation and Demodulation

```matlab
clc;
clear all;
close all;

f1 = input("Enter the frequency of Carrier 1 (Hz): ");
f2 = input("Enter the frequency of Carrier 2 (Hz): ");
f3 = input("Enter the frequency of Message signal (Hz): ");

t = 0:0.001:1;

m = (square(2*pi*f3*t) + 1) / 2;
c1 = sin(2*pi*f1*t);
c2 = sin(2*pi*f2*t);

s = zeros(1, length(t));

for i = 1:length(t)
    if m(i) == 1
        s(i) = c1(i);
    else
        s(i) = c2(i);
    end
end

subplot(3,2,1);
plot(t,m,'LineWidth',1.5);
title('Message Signal');
grid on;

subplot(3,2,2);
plot(t,c1,'LineWidth',1.5);
title('Carrier 1 Signal');
grid on;

subplot(3,2,3);
plot(t,c2,'LineWidth',1.5);
title('Carrier 2 Signal');
grid on;

subplot(3,2,4);
plot(t,s,'LineWidth',1.5);
title('FSK Modulated Signal');
grid on;

y2 = zeros(1,length(t));

for j = 1:length(t)
    if s(j) == c1(j)
        y2(j) = 1;
    else
        y2(j) = 0;
    end
end

subplot(3,2,5);
plot(t,y2,'LineWidth',1.5);
title('Demodulated FSK Signal');
grid on;
```

## Experiment 3: BPSK BER Analysis

```matlab
clc;
clear all;
close all;

N=10000000;
EbN0dB = -6:2:10;

data=randn(1,N)>=0;
bpskModulated = 2*data-1;

M=2;
Rm=log2(M);
Rc=1;

BER = zeros(1,length(EbN0dB));
index=1;

for k=EbN0dB
    EbN0 = 10.^(k/10);
    noiseSigma = sqrt(1./(2*Rm*Rc*EbN0));
    noise = noiseSigma*randn(1,length(bpskModulated));
    received = bpskModulated + noise;
    estimatedBits = (received>=0);
    BER(index) = sum(xor(data,estimatedBits))/length(data);
    index=index+1;
end

plotHandle=plot(EbN0dB,log10(BER),'r--');
set(plotHandle,'LineWidth',1.5);

title('SNR per bit Eb/N0 Vs BER Curve for BPSK');
xlabel('SNR per bit Eb/N0 in dB');
ylabel('Bit Error Rate BER in dB');
grid on;
hold on;

theoreticalBER = 0.5*erfc(sqrt(10.^(EbN0dB/10)));
plotHandle=plot(EbN0dB,log10(theoreticalBER),'k*');
set(plotHandle,'LineWidth',1.5);

legend('Simulated','Theoretical');
grid on;
```

## Experiment 4: DSSS

```matlab
clc;
clear all;
close all;

b = [1 0 1 0 1 0 1 0];
ln = length(b);

for i = 1:ln
    if b(i) == 0
        b(i) = -1;
    end
end

k = 1;
for i = 1:ln
    for j = 1:8
        bb(k) = b(i);
        k = k + 1;
    end
end

len = length(bb);

pr_sig = round(rand(1,len));

for i = 1:len
    if pr_sig(i) == 0
        pr_sig(i) = -1;
    end
end

bbs = bb .* pr_sig;

dsss = [];
t = 0:0.1/10:2*pi;

c1 = cos(t);
c2 = cos(t + pi);

for k = 1:len
    if bbs(k) == -1
        dsss = [dsss c1];
    else
        dsss = [dsss c2];
    end
end

figure;

subplot(3,1,1);
stairs(bb,'linewidth',2);
axis([0 len -2 3]);
title('Original Bit Sequence');
grid on;

subplot(3,1,2);
stairs(pr_sig,'linewidth',2);
axis([0 len -2 3]);
title('Pseudo Random Bit Sequence');
grid on;

subplot(3,1,3);
plot(dsss,'linewidth',1);
title('Spread Spectrum Signal DSSS');
grid on;
```
