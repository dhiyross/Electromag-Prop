%% Rosyiidah Dhiya'Ulhaq
%% 19/446468/TK/49573
%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%
%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%
%% informasi data yan digunakan
fi=8; % frekuensi informasi
fg=55; % frekuensi informasi geser
fc=fg-fi; % frekuensi carrier
Fs=2*fc; % frekuensi sampling
D=15; % daya pancar
T=1/Fs; % periode sampling
L=1000; % panjang sinyal
t=(0:L-1)*T; % waktu sampling
l=20000; % jarak pengirim ke penerima
axis_double=((-L)/2:L/2-1)*(Fs/L);

%% isyarat informasi
%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%
mt=D*cos(2*pi*fi*t);
M=fft(mt);
M_mag=2*(abs(M)./L);
M_double=fftshift(M_mag);
%% plot grafik
figure(1);
%% time domain 
subplot(2,1,1);
plot(t,mt);
title('Isyarat Informasi (Time Domain)');
xlim([0 10]);
xlabel('t(s)');
ylabel('Amplitude');
%% frequency domain
subplot(2,1,2);
plot(axis_double,M_double,'m');
title('Isyarat Informasi (Frequency Domain)');
xlabel('Frequency (Hz)');
ylabel('Magnitude');

%% isyarat carrier 
%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%
ct=D*cos(2*pi*fc*t);
C=fft(ct);
C_mag=2*(abs(C)./L);
C_double=fftshift(C_mag);
%% plot grafik
figure(2);
%% time domain
subplot(2,1,1);
plot(t,ct);
title('Isyarat Carrier (Time Domain)');
xlim([0 10]);
xlabel('t(s)');
ylabel('Amplitude');
%% frequency domain
subplot(2,1,2);
plot(axis_double,C_double,'m');
title('Isyarat Carrier (Frequency Domain)');
xlabel('Frequency (Hz)');
ylabel('Magnitude');


%% isyarat termodulasi
%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%
mod=mt.*ct; % sinyal isyarat termodulasi
M0=fft(mod);
M0_mag=2*(abs(M0)./L);
M0_double=fftshift(M0_mag);
%% plot grafik
figure(3);
%% time domain
subplot(2,1,1);
plot(t,mod);
title('Isyarat Termodulasi (Time Domain)');
xlim([0 10]);
xlabel('t(s)');
ylabel('Amplitude');

%% frequency domain
subplot(2,1,2);
plot(axis_double,M0_double,'m');
title('Isyarat Termodulasi (Frequency Domain)');
xlabel('Frequency (Hz)');
ylabel('Magnitude');


%% USB filter
%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%
f1=fg-2*fi; %lower cutoff frequency
f2=fg; %upper cutoff frequency
teta_1=2*pi*f1/Fs;
teta_2=2*pi*f2/Fs;
N=L;
n=(0:N-1);
%% FIR digital filter
h1=((teta_2/pi).* sinc(teta_2.*(n-0.5*N)/pi));
h2=((teta_1/pi).* sinc(teta_1.*(n-0.5*N)/pi));
hn=h1-h2;
H1=fft(hn);
H1_mag=2*(abs(H1)./N);
H1_double=fftshift(H1_mag);
%% plot grafik
figure(4)
%% time domain
subplot(2,1,1);
plot(n,hn);
title('USB Filter (Time Domain)');
xlabel('t(s)');
ylabel('Amplitude');
%% fequency domain
subplot(2,1,2);
plot(axis_double,H1_double,'m');
title('USB Filter (Frequency Domain)');
xlabel('Frequency (Hz)');
ylabel('Magnitude');


%% isyarat termodulasi terfilter
%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%
mf=M0.*H1;
mf_mag=2*(abs(mf)./L);
mf_double=fftshift(mf_mag);
mod_f=ifft(mf);
%% plot grafik
figure(5);
%% time domain
subplot(2,1,1);
plot(t,mod_f)
title('Isyarat Termodulasi Terfilter (Time domain)');
xlim([0 10]);
xlabel('t(s)');
ylabel('Amplitude');
%% frequency domain
subplot(2,1,2);
plot(axis_double,mf_double,'m');
title('Isyarat Termodulasi Terfilter (Frequency domain)');
xlabel('Frequency (Hz)');
ylabel('Magnitude');


%% Jalur Transmisi dan Isyarat Diterima
%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%
%% amplifier 1
amp1=0.0003;
mod_f= mod_f.*amp1;
%% atenuasi transmisi
lc=l/3;
aRG11_loss=3.18;
aRG6_loss=5.25;
aRG59_loss=6.4;
zRG11=22;
zRG6=28;
zRG59=35;
Loss_Cable=lc*(aRG11_loss+aRG6_loss+aRG59_loss)/100;
r1=abs((zRG11 - zRG6)/(zRG11 + zRG6)); %%R6-11
r2=abs((zRG6 - zRG59)/(zRG6 + zRG59)); %%R59-6
r3=r1+r2;
r_total_db = 10*log10(1/(1-r3^2));
Total_loss= 10^(-(Loss_Cable+ r_total_db)/10);
%% sinyal yang diterima
delta=zeros(1, 100);
delta(1)=1;
delta=Total_loss.*delta;
y=conv(mod_f,delta,'same');
yt=fft(y);
yt_mag=2*(abs(yt)/L);
yt_double=fftshift(yt_mag);
%% plot grafik
figure(6);
%% time domain
subplot(2,1,1);
plot(t,y)
title('Jalur Transmisi dan Isyarat Diterima (Time Domain)')
xlim([0 11]);
xlabel('t(s)');
ylabel('Amplitude');
%% frequency domain
subplot(2,1,2);
plot(axis_double,yt_double,'m');
title('Jalur Transmisi dan Isyarat Diterima (Frequency Domain)')
xlabel('Frequency (Hz)');
ylabel('Magnitude');

%% isyarat terdemodulasi
%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%
demod=y.*ct;
demod1=fft(demod);
demod1_mag=2*(abs(demod1)./L);
demod1_double = fftshift(demod1_mag);
%% plot grafik
figure(7);
%% time domain
subplot(2,1,1);
plot(t,demod);
title('Isyarat Terdemodulasi (Time Domain)')
xlim([0 11]);
xlabel('Waktu (s)')
ylabel('Amplitudo')
%% frequency domain
subplot(2,1,2);
plot(axis_double,demod1_double,'m');
title('Isyarat Terdemodulasi (Frequency Domain)')
xlabel('Frekuensi (MHz)')
ylabel('Magnitudo')


%% LP filter
%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%
teta1_lpf=0;
h1_lpf=((teta_2/pi).*sinc(teta_2*(n-0.5*N)/pi));
h2_lpf=((teta1_lpf/pi).*sinc(teta1_lpf*(n-0.5*N)/pi));
hn_lpf=h1_lpf-h2_lpf;
lpf= fft(hn_lpf);
lpf_mag=2*(abs(lpf)./L);
lpf_double = fftshift(lpf_mag);
%% plot grafik
figure(8);
%% time domain
subplot(2,1,1);
plot(n,hn_lpf);
title('Low pass Filter (Time Domain');
xlabel('Waktu (s)')
ylabel('Amplitudo')

%% frequency domain
subplot(2,1,2);
plot(axis_double,lpf_double,'m');
title('Low pass Filter (Frequency Domain');
xlabel('Frequency (Hz)');
ylabel('Magnitude');


%% isyarat terdemodulasi terfilter
%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%
%% Amplifier 2
amp2=D*1000/max(abs(lpf.*demod1));
%% recovered signal
recov_f=lpf.*demod1;
recov_f=recov_f.*amp2;
recov=ifft(recov_f);
recov_f_mag=2*abs(recov_f)./L;
recov_f_double=fftshift(recov_f_mag);
%% plot grafik
figure(9);
%% time domain
subplot(2,1,1);
plot(t,recov);
title('Isyarat Terdemodulasi Terfilter (Time domain)');
xlim([0 10]);
xlabel('time(s)');
ylabel('Amplitude');
%% frequency domain
subplot(2,1,2);
plot(axis_double,recov_f_double,'m');
title('Isyarat Terdemodulasi Terfilter (Frequency Domain)');
xlabel('Frequency (Hz)');
ylabel('Magnitude');
