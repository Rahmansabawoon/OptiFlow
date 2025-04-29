#include <stdio.h>
#include <limits.h>

#define N 4 
#define M 3 
int islem_sureleri[N][M] = {
    {2, 1, 4},
    {1, 4, 2},
    {2, 3, 1},
    {5, 9, 1}
};

int gecis_maliyetleri[M][M] = {
    {0, 3, 2},
    {3, 0, 4},
    {2, 4, 0}
};

int dp[N][M];

void hesapla_min_sure() {
    for (int j = 0; j < M; j++) {
        dp[0][j] = islem_sureleri[0][j];
    }
    for (int i = 1; i < N; i++) {
        for (int j = 0; j < M; j++) {
            dp[i][j] = INT_MAX;
            for (int k = 0; k < M; k++) {
                int maliyet = dp[i-1][k] + gecis_maliyetleri[k][j] + islem_sureleri[i][j];
                if (maliyet < dp[i][j]) {
                    dp[i][j] = maliyet;
                }
            }
        }
    }
    int min_sure = INT_MAX;
    for (int j = 0; j < M; j++) {
        if (dp[N-1][j] < min_sure) {
            min_sure = dp[N-1][j];
        }
    }
    printf("Minimum toplam süre: %d\n", min_sure);
}
int main() {
    hesapla_min_sure();
    return 0;
}
