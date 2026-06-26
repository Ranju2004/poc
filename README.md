From your uploaded **MVJ22EA43 - Principles of Communication Lab Manual**, here are the **11 experiment names**. The MATLAB programs are exactly as given in the manual. 

---

## Experiment 1: Amplitude Modulation and Demodulation

```matlab
% program for AM modulation
close all;
clear all;
clc;
fs=8000;
fm=20;
fc=500;
Am=1;
Ac=1;
t=[0:0.1*fs]/fs;
m=Am*cos(2*pi*fm*t);
c=Ac*cos(2*pi*fc*t);
ka=0.5;
u=ka*Am;
s1=Ac*(1+u*cos(2*pi*fm*t)).*cos(2*pi*fc*t);
subplot(4,3,1:3);
plot(t,m);
title('Modulating or Message signal(fm=20Hz)');
subplot(4,3,4:6);
plot(t,c);
title('Carrier signal(fc=500Hz)');
subplot(4,3,7);
plot(t,s1);
title('Under Modulated signal(ka.Am=0.5)');
Am=2;
ka=0.5;
u=ka*Am;
s2=Ac*(1+u*cos(2*pi*fm*t)).*cos(2*pi*fc*t);
subplot(4,3,8);
plot(t,s2);
title('Exact Modulated signal(ka.Am=1)');
Am=5;
ka=0.5;
u=ka*Am;
s3=Ac*(1+u*cos(2*pi*fm*t)).*cos(2*pi*fc*t);
subplot(4,3,9);
plot(t,s3);
title('Over Modulated signal(ka.Am=2.5)');

% program for AM Demodulation
r1=s1.*c;
[b a]=butter(1,0.01);
mr1=filter(b,a,r1);
subplot(4,3,10);
plot(t,mr1);
title('deModulated signal for(ka.Am=0.5)');

r2=s2.*c;
[b a]=butter(1,0.01);
mr2=filter(b,a,r2);
subplot(4,3,11);
plot(t,mr2);
title('deModulated signal for(ka.Am=1)');

r3=s3.*c;
[b a]=butter(1,0.01);
mr3=filter(b,a,r3);
subplot(4,3,12);
plot(t,mr3);
title('deModulated signal for(ka.Am=2.5)');
```

---

## Experiment 2: Frequency Modulation and Demodulation

```matlab
close all;
clear all;
clc;

% Parameters
fs = 10000;
Ac = 1;
Am = 1;
fm = 35;
fc = 500;
B = 10;

t = (0:(1/fs):0.1);

wm = 2*pi*fm;
m_t = Am*cos(wm*t);

subplot(4,1,1);
plot(t,m_t);
title('Modulating or Message signal (fm=35Hz)');
xlabel('Time (s)');
ylabel('Amplitude');
grid on;

wc = 2*pi*fc;
c_t = Ac*cos(wc*t);

subplot(4,1,2);
plot(t,c_t);
title('Carrier signal (fc=500Hz)');
xlabel('Time (s)');
ylabel('Amplitude');
grid on;

s_t = Ac*cos(wc*t + B*sin(wm*t));

subplot(4,1,3);
plot(t,s_t);
title('FM Modulated signal');
xlabel('Time (s)');
ylabel('Amplitude');
grid on;

frequencyDeviation = B*fm;
d = fmdemod(s_t,fc,fs,frequencyDeviation);

subplot(4,1,4);
plot(t,d);
title('Demodulated signal');
xlabel('Time (s)');
ylabel('Amplitude');
grid on;
```

---

## Experiment 3: DSB-SC Modulator & Detector

```matlab
close all
clear all
clc

t=0:0.000001:.001;
Vm=1;
Vc=1;
fm=2000;
fc=50000;

m_t=Vm*sin(2*pi*fm*t);
subplot(4,1,1);
plot(t,m_t);

c_t=Vc*sin(2*pi*fc*t);
subplot(4,1,2);
plot(t,c_t);

subplot(4,1,3);
s_t=m_t.*c_t;
hold on;
plot(t,s_t);
plot(t,m_t,'r:');
plot(t,-m_t,'r:');
hold off;

r=s_t.*c_t;
[b a]=butter(1,0.01);
mr=filter(b,a,r);

subplot(4,1,4);
plot(t,mr);
```

---

## Experiment 4: Simulation of NRZ & RZ

```matlab
clc;
close all;
clear all;

% NRZ polar line coding
n=[1 0 1 0];

nn=zeros(1,length(n));

for m=1:length(n)
    if n(m)==0
        nn(m)=-1;
    else
        nn(m)=1;
    end
end

i=1;
t=0:0.01:length(n);
y=zeros(1,length(t));

for j=1:length(t)
    if t(j)<=i
        y(j)=nn(i);
    else
        i=i+1;
    end
end

figure;
subplot(2,1,1);
plot(t,y,'b','LineWidth',1.5);
axis([0 length(n) -2 2]);
title('NRZ Polar Line Coding');
xlabel('Time');
ylabel('Amplitude');
grid on;

% RZ polar line coding
n=randi([0 1],1,10);

nn=zeros(1,length(n));

for k=1:length(n)
    if n(k)==0
        nn(k)=-1;
    else
        nn(k)=1;
    end
end

i=1;
a=0;
b=0.5;
t=0:0.01:length(n);
y=zeros(1,length(t));

for j=1:length(t)
    if t(j)>=a && t(j)<=b
        y(j)=nn(i);
    elseif t(j)>b && t(j)<=i
        y(j)=0;
    else
        i=i+1;
        a=a+1;
        b=b+1;
    end
end

subplot(2,1,2);
plot(t,y,'r','LineWidth',1.5);
axis([0 length(n) -2 2]);
title('RZ Polar Line Coding');
xlabel('Time');
ylabel('Amplitude');
grid on;
Here are **Experiment 5–11 names and copyable programs** from your manual. 

## 05. EYE DIAGRAM

```matlab
N=100;
X=2*round(rand(N,1))-1;
X1=X';
a=-5.5:1/100:1.5;
b=-3.5:1/100:3.5;
c=-1.5:1/100:5.5;
for i=1:1:(N+2-11);
d=X1(1,i)*sinc(b);
e=X1(1,i+1)*sinc(b);
f=X1(1,i+2)*sinc(b);
hold on, plot(a,f);
hold on, plot(b,e);
hold on, plot(c,d);
end
title('Eye Diagram - Before Equalization'); xlabel('Time(s)');
ylabel('Amplitude'); axis([-1 1 -2 2])
```

## 06. SIMULATION OF ASK GENERATION & DETECTION SCHEMES

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
title('ASKSIGNAL');
xlabel('t---->');
ylabel('s(t)');
grid on;
% ASK Demodulation
y_dem =c.*s;
t4=0:0.001:1;
z=square(y_dem); % intregation
%A_dem=round((2*z/0.001));
for i=0:1000
 if(y_dem(i+1)>0)
 X(i+1)=1;
 else
X(i+1)=0;
 end
end
subplot(5,1,4);
plot(t,X)
subplot(5,1,5);
plot(t,X)
title('ASK Demodulated signal');
xlabel('t--->');
ylabel('b(n)');
```

## 07. SIMULATION OF FSK GENERATION & DETECTION SCHEMES

```matlab
clc;
clear all;
close all;
% Input parameters
f1 = input("Enter the frequency of Carrier 1 (Hz): ");
f2 = input("Enter the frequency of Carrier 2 (Hz): ");
f3 = input("Enter the frequency of Message signal (Hz): ");
t = 0:0.001:1; % Time vector

% Generate the message signal
m = (square(2*pi*f3*t) + 1) / 2; % Binary message signal (0 and 1)
% Generate carrier signals
c1 = sin(2*pi*f1*t); % Carrier signal 1
c2 = sin(2*pi*f2*t); % Carrier signal 2
% FSK Modulation
s = zeros(1, length(t)); % Initialize FSK signal
for i = 1:length(t)
 if m(i) == 1
 s(i) = c1(i); % Use Carrier 1 for binary 1
 else
 s(i) = c2(i); % Use Carrier 2 for binary 0
 end
end
% Plot the message signal
subplot(3, 2, 1);
plot(t, m, 'LineWidth', 1.5);
xlabel('Time (s)');
ylabel('Amplitude');
title('Message Signal');
grid on;
% Plot Carrier 1
subplot(3, 2, 2);
plot(t, c1, 'LineWidth', 1.5);
xlabel('Time (s)');
ylabel('Amplitude');
title('Carrier 1 Signal');
grid on;
% Plot Carrier 2
subplot(3, 2, 3);
plot(t, c2, 'LineWidth', 1.5);
xlabel('Time (s)');
ylabel('Amplitude');
title('Carrier 2 Signal');
grid on;
% Plot FSK Modulated Signal
subplot(3, 2, 4);
plot(t, s, 'LineWidth', 1.5);
xlabel('Time (s)');
ylabel('Amplitude');
title('FSK Modulated Signal');
grid on;
% FSK Demodulation
y2 = zeros(1, length(t)); % Initialize demodulated signal
for j = 1:length(t)
 if s(j) == c1(j)
 y2(j) = 1; % Detect binary 1
 else
 y2(j) = 0; % Detect binary 0
 end
end
% Plot FSK Demodulated Signal
subplot(3, 2, 5);
plot(t, y2, 'LineWidth', 1.5);
xlabel('Time (s)');
ylabel('Amplitude');
title('Demodulated FSK Signal');
grid on;
```

## 08. ERROR PERFORMANCE OF BPSK

```matlab
% Demonstration of Eb/N0 Vs BER for BPSK modulation scheme
clear;
clc;
%---------Input Fields------------------------
N=10000000; %Number of input bits
EbN0dB = -6:2:10; % Eb/N0 range in dB for simulation
%---------------------------------------------
data=randn(1,N)>=0; %Generating a uniformly distributed random 1s and 0s
bpskModulated = 2*data-1; %Mapping 0->-1 and 1->1
M=2; %Number of Constellation points M=2^k for BPSK k=1
Rm=log2(M); %Rm=log2(M) for BPSK M=2
Rc=1; %Rc = code rate for a coded system. Since no coding is used Rc=1
BER = zeros(1,length(EbN0dB)); %Place holder for BER values for each Eb/N0
index=1;
for k=EbN0dB,
%-------------------------------------------
%Channel Noise for various Eb/N0
%-------------------------------------------
%Adding noise with variance according to the required Eb/N0
EbN0 = 10.^(k/10); %Converting Eb/N0 dB value to linear scale
noiseSigma = sqrt(1./(2*Rm*Rc*EbN0)); %Standard deviation for AWGN Noise
noise = noiseSigma*randn(1,length(bpskModulated));
received = bpskModulated + noise;
%-------------------------------------------
%Threshold Detector
estimatedBits=(received>=0);
%------------------------------------------
%Bit Error rate Calculation
BER(index) = sum(xor(data,estimatedBits))/length(data);
index=index+1;
end
%Plot commands follows
plotHandle=plot(EbN0dB,log10(BER),'r--');
set(plotHandle,'LineWidth',1.5);
title('SNR per bit (Eb/N0) Vs BER Curve for BPSK Modulation Scheme');
xlabel('SNR per bit (Eb/N0) in dB');
ylabel('Bit Error Rate (BER) in dB');
grid on;
hold on;
theoreticalBER = 0.5*erfc(sqrt(10.^(EbN0dB/10)));
plotHandle=plot(EbN0dB,log10(theoreticalBER),'k*');
set(plotHandle,'LineWidth',1.5);
legend('Simulated','Theoretical');
grid on;
```

## 09. ERROR PERFORMANCE OF QPSK

```matlab
% QPSK MODULATION AND BER ESTIMATION IN AWGN CHANNEL
clc; clear all; close all;
N=1e6; % Number of bits transmited
SNRdB= 0:1:20; % SNR for simulation
SNRlin=10.^(SNRdB/10);
BER = zeros(1,length(SNRlin));% simulated BER
SER = zeros(1,length(SNRlin));% simulated SER
b1 = rand(1,N) > 0.5;
b2 = rand(1,N) > 0.5;
% QPSK symbol mapping
I = (2*b1) - 1;
Q = (2*b2) - 1;
S = I + 1j*Q;
N0 = 1./SNRlin; % Variance
for k = 1:length(SNRdB)
noise = sqrt(N0(k)/2)*(randn(1,N) + 1j*randn(1,N)); % AWGN noise
sig_Rx = S + noise; % Recived signal
% For BER calculation
sig_I = real(sig_Rx); % I component
sig_Q = imag(sig_Rx); % Q component
bld_I = sig_I > 0; % I decision
bld_Q = sig_Q > 0; % Q decision
b1_error = (bld_I ~= b1); % Inphase bit error
b2_error = (bld_Q ~= b2); % Quadrature bit error
Error_bit = sum(b1_error) + sum(b2_error); % Total bit error
BER(k) = sum(Error_bit)/(2*N); % Simulated BER
% For SER calculation
error_symbol = or(b1_error, b2_error); % if bit in I or bit in Q either wrong than error
SER(k) = sum(error_symbol)/N;
end
BER_theo = 2*qfunc(sqrt(2*SNRlin)); % Theoretical BER
SER_theo = 2*qfunc(sqrt(2*SNRlin)) - (qfunc(sqrt(2*SNRlin))).^2; % Theoretical SER
figure(1);
semilogy(SNRdB, BER_theo,'r-')
hold on
semilogy(SNRdB, BER,'k*')
xlabel('SNR[dB]')
ylabel('Bit Error Rate');
legend('Theoretical', 'Simulated');
title(['Probability of Bit Error for QPSK Modulation']);
grid on;
hold off;
figure(2);
semilogy(SNRdB, SER_theo,'r-')
hold on
semilogy(SNRdB, SER,'k*')
xlabel('SNR[dB]')
ylabel('Symbol Error Rate');
legend('Theoretical', 'Simulated');
title(['Probability of symbol Error for QPSK Modulation']);
grid on;
hold off;
```

## 10. SIMULATION OF DSSS GENERATION SCHEMES

```matlab
clc;
close all;
clear all;
% Input bit sequence
b = [1 0 1 0 1 0 1 0];
ln = length(b);
% Convert bit 0 to -1
for i = 1:ln
 if b(i) == 0
 b(i) = -1;
 end
end
% Generate the bit sequence with each bit having 8 samples
k = 1;
for i = 1:ln
 for j = 1:8
 bb(k) = b(i);
 k = k + 1;
 end
end
% Length of expanded bit sequence
len = length(bb);
% Generate the pseudo-random bit sequence for spreading
pr_sig = round(rand(1, len)); % Generate 0 or 1
for i = 1:len
 if pr_sig(i) == 0
 pr_sig(i) = -1; % Convert 0 to -1
 end
end
% Multiply bit sequence with pseudo-random sequence
bbs = bb .* pr_sig;
% Modulate the spread spectrum signal
dsss = [];
t = 0:0.1/10:2*pi;
c1 = cos(t); % Carrier for bit -1
c2 = cos(t + pi); % Carrier for bit 1
for k = 1:len
 if bbs(k) == -1
 dsss = [dsss c1]; % Use carrier c1 for -1
 else
 dsss = [dsss c2]; % Use carrier c2 for 1
 end
end
% Subfigure 1: Original Bit Sequence
figure;
subplot(3, 1, 1);
stairs(bb, 'linewidth', 2);
axis([0 len -2 3]);
title('Original Bit Sequence b(t)');
xlabel('Time');
ylabel('Amplitude');
grid on;
% Subfigure 2: Pseudo-random Bit Sequence
subplot(3, 1, 2);
stairs(pr_sig, 'linewidth', 2);
axis([0 len -2 3]);
title('Pseudo-random Bit Sequence pr\_sig(t)');
xlabel('Time');
ylabel('Amplitude');
grid on;
% Subfigure 3: Spread Spectrum Signal
subplot(3, 1, 3);
plot(dsss, 'linewidth', 1);
title('Spread Spectrum Signal (DSSS)');
xlabel('Time');
ylabel('Amplitude');
grid on;
```
<img width="561" height="389" alt="image" src="https://github.com/user-attachments/assets/f979d74e-95eb-426f-886b-3b2ea455f784" />

<img width="499" height="811" alt="image" src="https://github.com/user-attachments/assets/52ee2ad4-73ff-471a-8830-0b1fe56ffd54" />

<img width="383" height="624" alt="image" src="https://github.com/user-attachments/assets/7c9d9ae4-ae3d-4b20-afed-2fe15a1d6da1" />


 
