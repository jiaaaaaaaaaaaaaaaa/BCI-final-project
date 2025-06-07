fs = EEG.srate;

nTime = size(EEG.data, 2);

nEpochs = size(EEG.data, 3);

freqs = (0:nTime-1)*(fs/nTime);

freqs = freqs(1:floor(nTime/2)+1);

alpha_idx = find(freqs >= 8 & freqs <= 13);

theta_idx = find(freqs >= 4 & freqs <= 7);

%channel index

ch_Fp1 = find(strcmpi({EEG.chanlocs.labels}, 'Fp1'));

ch_Fp2 = find(strcmpi({EEG.chanlocs.labels}, 'Fp2'));

ch_Fz  = find(strcmpi({EEG.chanlocs.labels}, 'Fz'));

ch_Pz  = find(strcmpi({EEG.chanlocs.labels}, 'Pz'));

alpha_power = zeros(2, nEpochs);  % Fp1, Fp2

theta_power = zeros(2, nEpochs);  % Fz, Pz

for ep = 1:nEpochs
    % Fp1 - alpha
    Y = fft(squeeze(EEG.data(ch_Fp1, :, ep)));
    P = abs(Y/nTime).^2;
    P = P(1:floor(nTime/2)+1);
    P(2:end-1) = 2*P(2:end-1);
    alpha_power(1, ep) = mean(P(alpha_idx));

    % Fp2 - alpha
    Y = fft(squeeze(EEG.data(ch_Fp2, :, ep)));
    P = abs(Y/nTime).^2;
    P = P(1:floor(nTime/2)+1);
    P(2:end-1) = 2*P(2:end-1);
    alpha_power(2, ep) = mean(P(alpha_idx));

    % Fz - theta
    Y = fft(squeeze(EEG.data(ch_Fz, :, ep)));
    P = abs(Y/nTime).^2;
    P = P(1:floor(nTime/2)+1);
    P(2:end-1) = 2*P(2:end-1);
    theta_power(1, ep) = mean(P(theta_idx));

    % Pz - theta
    Y = fft(squeeze(EEG.data(ch_Pz, :, ep)));
    P = abs(Y/nTime).^2;
    P = P(1:floor(nTime/2)+1);
    P(2:end-1) = 2*P(2:end-1);
    theta_power(2, ep) = mean(P(theta_idx));
end

% 平均 alpha / theta power

mean_alpha = mean(alpha_power, 2); 

mean_theta = mean(theta_power, 2); 

figure;

subplot(1,2,1);

bar(mean_alpha);

xticklabels({'Fp1','Fp2'});

ylabel('Alpha Power (8–13 Hz)');

title('Alpha Power per Channel');

subplot(1,2,2);

bar(mean_theta);

xticklabels({'Fz','Pz'});

ylabel('Theta Power (4–7 Hz)');

title('Theta Power per Channel');

mean_alpha

mean_theta

% 重複五位低錯誤率參與者
low_alpha = [];  

low_theta = [];

low_alpha(:, i) = mean_alpha;

low_theta(:, i) = mean_theta;

% 重複五位高錯誤率參與者
high_alpha = [];  

high_theta = [];

high_alpha(:, i) = mean_alpha;

high_theta(:, i) = mean_theta;

low_alpha_avg = mean(low_alpha, 2);

high_alpha_avg = mean(high_alpha, 2);

low_theta_avg = mean(low_theta, 2);

high_theta_avg = mean(high_theta, 2);

mean_low_alpha = mean(low_alpha, 1);

mean_high_alpha = mean(high_alpha, 1);

mean_low_theta = mean(low_theta, 1);

mean_high_theta = mean(high_theta, 1);


figure;

subplot(1,2,1);  % Alpha

bar([mean_low_alpha; mean_high_alpha]');

legend('Low Error', 'High Error');

xticklabels({'Fp1','Fp2'});

ylabel('Alpha Power');

title('Alpha Power - Low vs High Error');

subplot(1,2,2);  % Theta

bar([mean_low_theta; mean_high_theta]');

legend('Low Error', 'High Error');

xticklabels({'Fz','Pz'});

ylabel('Theta Power');

title('Theta Power - Low vs High Error');

% T test
[~, p_alpha, ~, stats_alpha] = ttest2(low_alpha_avg, high_alpha_avg);

[~, p_theta, ~, stats_theta] = ttest2(low_theta_avg, high_theta_avg);


fprintf('Alpha t-test: t = %.3f, p = %.4f\n', stats_alpha.tstat, p_alpha);

fprintf('Theta t-test: t = %.3f, p = %.4f\n', stats_theta.tstat, p_theta);

figure;

subplot(1,2,1);

bar([mean(low_alpha_avg), mean(high_alpha_avg)]);

set(gca, 'XTickLabel', {'Low Error', 'High Error'});

ylabel('Alpha Power (Fp1+Fp2 avg)');

title(sprintf('Alpha (p = %.4f)', p_alpha));

subplot(1,2,2);

bar([mean(low_theta_avg), mean(high_theta_avg)]);

set(gca, 'XTickLabel', {'Low Error', 'High Error'});

ylabel('Theta Power (Fz+Pz avg)');

title(sprintf('Theta (p = %.4f)', p_theta));
