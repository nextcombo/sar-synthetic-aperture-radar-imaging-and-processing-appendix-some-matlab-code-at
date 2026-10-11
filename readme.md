# [SAR] Synthetic Aperture Radar Imaging and Processing [Appendix: Some MATLAB Code at the End]

MATLAB simulation results: chirp_sig.m
clear all;\n%%%  parameters' definition\nc=3e+8;                    % speed of light\npi=3.1415926; \nj=sqrt(-1);  \n​\nTp=1.e-6;                 % transmitted pulse width      \nfc=1.e+9;                    % carrier frequency \nBr=50.e+6;              % transmitted bandwidth\nFs=200.e+6;             % A/D sample rate\nkr=Br/Tp;               % range chirp rate\n​\nNr=Tp*Fs;\nNi=1:Nr;\ntr=(Ni-Nr/2)*Tp/Nr;\n​\n%===============================\n%Generate a Chirp pulse\n%===============================\n​\nsig = exp(j*pi*kr*(tr).^2);\n​\nfigure; \nsubplot(2,3,1); plot(real(sig));\nsubplot(2,3,2); plot(imag(sig));\n​\n%===============================\n% Spectrum of this Chirp pulse\n%===============================\n​\nsig_spec=fftshift(fft(sig));\nsubplot(2,3,3); ; plot(abs(sig_spec));\n​\n%===============================\n%Match filtering in time domain\n%===============================\n​\nmf_sig = conj(fliplr(sig));\nsubplot(2,3,4);  plot(real(mf_sig));\nsubplot(2,3,5);  plot(imag(mf_sig));\n​\nmf_out = conv(sig, mf_sig);\nsubplot(2,3,6);  plot(abs(mf_out(Nr/2+1:Nr*3/2)));\n​\npause;\n%=====================================\n%Match filtering in frequency domain\n%=====================================\n​\nfr=(Ni-Nr/2)*Fs/Nr;\nmf_spec=exp(j*pi*fr.^2/kr);\nmf_spec_out=ifft(fftshift(sig_spec.*mf_spec));\n​\nfigure; \nsubplot(1,2,1); plot(abs(mf_spec_out));\n​\nsig_un=20*log10(abs(mf_spec_out)/max(abs(mf_spec_out)));\nfor i=1 :Nr\n    if (sig_un(i)<-40 )\n        sig_un(i)=-40;\n    end \nend\nsubplot(1,2,2); plot(sig_un);\n​\n\n  
range_compress.m  
clear all;\n%%%  parameters' definition\nc=3e+8;                    % speed of light\npi=3.1415926; \nj=sqrt(-1);  \n​\nTp=1.e-6;                 % transmitted pulse width      \nfc=1.e+9;                    % carrier frequency \nBr=50.e+6;              % transmitted bandwidth\nFs=200.e+6;             % A/D sample rate\nkr=Br/Tp;               % range chirp rate\n​\nNr=Tp*Fs;\nNi=1:Nr;\ntr=(Ni-Nr/2)*Tp/Nr;\n​\n%===============================\n%Chirp pulse echo from point A\n%===============================\n​\nsig_point0 = exp(j*pi*kr*(tr).^2);\n​\n%===============================\n%Chirp pulse echo from point B\n%===============================\n​\ndr=3;  dr_t=2*dr/c;  dN=dr_t*Fs;\nsig_point1 = exp(j*pi*kr*(tr-dr_t).^2);\n​\nsig_0 = zeros(1, 3*Nr); sig_1 = sig_0; sum_sig = sig_0;\n​\nsig_0(Nr+1:2*Nr)=sig_point0;\nsig_1(Nr+dN+1:2*Nr+dN)=sig_point1;\n​\n%===============================\n% Summary echo signal of A and B\n%===============================\n​\nsum_sig = sig_0 + sig_1;\n​\nfigure;\nsubplot(4,1,1); plot(real(sig_0));\nsubplot(4,1,2); plot(real(sig_1));\nsubplot(4,1,3); plot(real(sum_sig));\n​\n%=====================================\n% Range compression with match filter\n%=====================================\n​\nmf_sig = conj(fliplr(sig_point0));\nmf_out = conv(sum_sig, mf_sig);\nNs=Nr/2+1; Ne=3*Nr+Nr/2;\nsubplot(4,1,4); plot(abs(mf_out(Ns:Ne)));\n\n  
range_migration.m​  
sar_echo.m  

## Images

![[SAR] Synthetic Aperture Radar Imaging and Processing [Appendix: Some MATLAB Code at the End]](01.jpg)
![[SAR] Synthetic Aperture Radar Imaging and Processing [Appendix: Some MATLAB Code at the End]](02.jpg)
![[SAR] Synthetic Aperture Radar Imaging and Processing [Appendix: Some MATLAB Code at the End]](03.jpg)
![[SAR] Synthetic Aperture Radar Imaging and Processing [Appendix: Some MATLAB Code at the End]](04.jpg)
![[SAR] Synthetic Aperture Radar Imaging and Processing [Appendix: Some MATLAB Code at the End]](05.jpg)
![[SAR] Synthetic Aperture Radar Imaging and Processing [Appendix: Some MATLAB Code at the End]](06.jpg)
![[SAR] Synthetic Aperture Radar Imaging and Processing [Appendix: Some MATLAB Code at the End]](07.jpg)
![[SAR] Synthetic Aperture Radar Imaging and Processing [Appendix: Some MATLAB Code at the End]](08.jpg)
![[SAR] Synthetic Aperture Radar Imaging and Processing [Appendix: Some MATLAB Code at the End]](09.jpg)
![[SAR] Synthetic Aperture Radar Imaging and Processing [Appendix: Some MATLAB Code at the End]](10.jpg)
![[SAR] Synthetic Aperture Radar Imaging and Processing [Appendix: Some MATLAB Code at the End]](11.jpg)
![[SAR] Synthetic Aperture Radar Imaging and Processing [Appendix: Some MATLAB Code at the End]](12.jpg)
![[SAR] Synthetic Aperture Radar Imaging and Processing [Appendix: Some MATLAB Code at the End]](13.jpg)
![[SAR] Synthetic Aperture Radar Imaging and Processing [Appendix: Some MATLAB Code at the End]](14.jpg)
![[SAR] Synthetic Aperture Radar Imaging and Processing [Appendix: Some MATLAB Code at the End]](15.jpg)
![[SAR] Synthetic Aperture Radar Imaging and Processing [Appendix: Some MATLAB Code at the End]](16.jpg)
![[SAR] Synthetic Aperture Radar Imaging and Processing [Appendix: Some MATLAB Code at the End]](17.jpg)
![[SAR] Synthetic Aperture Radar Imaging and Processing [Appendix: Some MATLAB Code at the End]](18.jpg)
![[SAR] Synthetic Aperture Radar Imaging and Processing [Appendix: Some MATLAB Code at the End]](19.jpg)
![[SAR] Synthetic Aperture Radar Imaging and Processing [Appendix: Some MATLAB Code at the End]](20.jpg)
![[SAR] Synthetic Aperture Radar Imaging and Processing [Appendix: Some MATLAB Code at the End]](21.jpg)
![[SAR] Synthetic Aperture Radar Imaging and Processing [Appendix: Some MATLAB Code at the End]](22.jpg)
![[SAR] Synthetic Aperture Radar Imaging and Processing [Appendix: Some MATLAB Code at the End]](23.jpg)
![[SAR] Synthetic Aperture Radar Imaging and Processing [Appendix: Some MATLAB Code at the End]](24.jpg)
![[SAR] Synthetic Aperture Radar Imaging and Processing [Appendix: Some MATLAB Code at the End]](25.jpg)
![[SAR] Synthetic Aperture Radar Imaging and Processing [Appendix: Some MATLAB Code at the End]](26.jpg)
![[SAR] Synthetic Aperture Radar Imaging and Processing [Appendix: Some MATLAB Code at the End]](27.jpg)
![[SAR] Synthetic Aperture Radar Imaging and Processing [Appendix: Some MATLAB Code at the End]](28.jpg)
![[SAR] Synthetic Aperture Radar Imaging and Processing [Appendix: Some MATLAB Code at the End]](29.jpg)
![[SAR] Synthetic Aperture Radar Imaging and Processing [Appendix: Some MATLAB Code at the End]](30.jpg)
![[SAR] Synthetic Aperture Radar Imaging and Processing [Appendix: Some MATLAB Code at the End]](31.jpg)
![[SAR] Synthetic Aperture Radar Imaging and Processing [Appendix: Some MATLAB Code at the End]](32.jpg)
![[SAR] Synthetic Aperture Radar Imaging and Processing [Appendix: Some MATLAB Code at the End]](33.jpg)
![[SAR] Synthetic Aperture Radar Imaging and Processing [Appendix: Some MATLAB Code at the End]](34.jpg)

<!-- PAYMENT_BLOCK -->

## Get this dataset

- Payment link (Stripe): [Buy now](https://buy.stripe.com/3cs8yP7sY87d0vu9AB)
- Payment QR code: ![Payment QR code](pay.png)

<!-- /PAYMENT_BLOCK -->
