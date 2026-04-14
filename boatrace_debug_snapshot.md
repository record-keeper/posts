# ClaudeDebug スナップショット

## 🟢 現状: GREEN

**生成**: 2026-04-15T07:00:01.765384+09:00

### 次に取るべきアクション
> 特になし。運用継続。

### 問題なし、運用継続してOK。

---

## 🔧 AI デバッグキュー（このClaudeが対処）

### 🟡 HEALTH_CHECK_FAIL  ×1  [2026-04-15T07:00:02]
- key: `HEALTH_CHECK_FAIL`
- **FIX**: health.py の check 失敗→対応する check 名から該当テーブル/指標を確認

### 🔴 ROI_CRITICAL  ×1  [2026-04-15T06:03:28]
- key: `ROI_CRITICAL|TEST_AUDIT_PHASE2`
- **FIX**: 該当戦略を strategies.json で enabled:false に→N≥300 Wilson下限<1.0確定のため

### 🔴 ROI_CRITICAL  ×1  [2026-04-15T06:01:31]
- key: `ROI_CRITICAL|TEST_AUDIT_IGNORE`
- **FIX**: 該当戦略を strategies.json で enabled:false に→N≥300 Wilson下限<1.0確定のため

### 🔴 STRATEGY_COLLAPSE  ×5  [2026-04-15T05:37:57]
- key: `STRATEGY_COLLAPSE|2026-04-13 017R combo=1 を 4 戦略が同時採用 → 分散効果ゼロ`
- **FIX**: 4戦略以上が同 combo を採用。v18 仕様的には許容。気になれば資金配分で分散制御

### 🔴 STRATEGY_COLLAPSE  ×5  [2026-04-15T05:37:57]
- key: `STRATEGY_COLLAPSE|2026-04-14 024R combo=1 を 6 戦略が同時採用 → 分散効果ゼロ`
- **FIX**: 4戦略以上が同 combo を採用。v18 仕様的には許容。気になれば資金配分で分散制御

### 🔴 STRATEGY_COLLAPSE  ×5  [2026-04-15T05:37:57]
- key: `STRATEGY_COLLAPSE|2026-04-14 029R combo=1 を 6 戦略が同時採用 → 分散効果ゼロ`
- **FIX**: 4戦略以上が同 combo を採用。v18 仕様的には許容。気になれば資金配分で分散制御

### 🔴 STRATEGY_COLLAPSE  ×5  [2026-04-15T05:37:57]
- key: `STRATEGY_COLLAPSE|2026-04-12 0411R combo=1 を 4 戦略が同時採用 → 分散効果ゼロ`
- **FIX**: 4戦略以上が同 combo を採用。v18 仕様的には許容。気になれば資金配分で分散制御

### 🔴 STRATEGY_COLLAPSE  ×5  [2026-04-15T05:37:57]
- key: `STRATEGY_COLLAPSE|2026-04-11 069R combo=1-5-4 を 4 戦略が同時採用 → 分散効果ゼロ`
- **FIX**: 4戦略以上が同 combo を採用。v18 仕様的には許容。気になれば資金配分で分散制御

### 🔴 STRATEGY_COLLAPSE  ×5  [2026-04-15T05:37:57]
- key: `STRATEGY_COLLAPSE|2026-04-12 066R combo=1-4-2 を 4 戦略が同時採用 → 分散効果ゼロ`
- **FIX**: 4戦略以上が同 combo を採用。v18 仕様的には許容。気になれば資金配分で分散制御

### 🔴 STRATEGY_COLLAPSE  ×5  [2026-04-15T05:37:57]
- key: `STRATEGY_COLLAPSE|2026-04-14 103R combo=1 を 5 戦略が同時採用 → 分散効果ゼロ`
- **FIX**: 4戦略以上が同 combo を採用。v18 仕様的には許容。気になれば資金配分で分散制御

### 🔴 STRATEGY_COLLAPSE  ×5  [2026-04-15T05:37:57]
- key: `STRATEGY_COLLAPSE|2026-04-11 119R combo=1 を 5 戦略が同時採用 → 分散効果ゼロ`
- **FIX**: 4戦略以上が同 combo を採用。v18 仕様的には許容。気になれば資金配分で分散制御

### 🔴 STRATEGY_COLLAPSE  ×5  [2026-04-15T05:37:57]
- key: `STRATEGY_COLLAPSE|20260410 117R combo=1-4-3 を 4 戦略が同時採用 → 分散効果ゼロ`
- **FIX**: 4戦略以上が同 combo を採用。v18 仕様的には許容。気になれば資金配分で分散制御

### 🔴 STRATEGY_COLLAPSE  ×5  [2026-04-15T05:37:57]
- key: `STRATEGY_COLLAPSE|2026-04-11 144R combo=1 を 4 戦略が同時採用 → 分散効果ゼロ`
- **FIX**: 4戦略以上が同 combo を採用。v18 仕様的には許容。気になれば資金配分で分散制御

### 🔴 STRATEGY_COLLAPSE  ×5  [2026-04-15T05:37:57]
- key: `STRATEGY_COLLAPSE|2026-04-11 1410R combo=1 を 4 戦略が同時採用 → 分散効果ゼロ`
- **FIX**: 4戦略以上が同 combo を採用。v18 仕様的には許容。気になれば資金配分で分散制御

### 🔴 STRATEGY_COLLAPSE  ×5  [2026-04-15T05:37:57]
- key: `STRATEGY_COLLAPSE|2026-04-12 145R combo=1 を 4 戦略が同時採用 → 分散効果ゼロ`
- **FIX**: 4戦略以上が同 combo を採用。v18 仕様的には許容。気になれば資金配分で分散制御

### 🔴 STRATEGY_COLLAPSE  ×5  [2026-04-15T05:37:57]
- key: `STRATEGY_COLLAPSE|2026-04-12 148R combo=1 を 6 戦略が同時採用 → 分散効果ゼロ`
- **FIX**: 4戦略以上が同 combo を採用。v18 仕様的には許容。気になれば資金配分で分散制御

### 🔴 STRATEGY_COLLAPSE  ×5  [2026-04-15T05:37:57]
- key: `STRATEGY_COLLAPSE|2026-04-13 147R combo=1 を 5 戦略が同時採用 → 分散効果ゼロ`
- **FIX**: 4戦略以上が同 combo を採用。v18 仕様的には許容。気になれば資金配分で分散制御

### 🔴 STRATEGY_COLLAPSE  ×5  [2026-04-15T05:37:57]
- key: `STRATEGY_COLLAPSE|2026-04-13 1411R combo=1 を 5 戦略が同時採用 → 分散効果ゼロ`
- **FIX**: 4戦略以上が同 combo を採用。v18 仕様的には許容。気になれば資金配分で分散制御

### 🔴 STRATEGY_COLLAPSE  ×5  [2026-04-15T05:37:57]
- key: `STRATEGY_COLLAPSE|2026-04-14 142R combo=1 を 5 戦略が同時採用 → 分散効果ゼロ`
- **FIX**: 4戦略以上が同 combo を採用。v18 仕様的には許容。気になれば資金配分で分散制御

### 🔴 STRATEGY_COLLAPSE  ×5  [2026-04-15T05:37:57]
- key: `STRATEGY_COLLAPSE|2026-04-11 159R combo=1 を 4 戦略が同時採用 → 分散効果ゼロ`
- **FIX**: 4戦略以上が同 combo を採用。v18 仕様的には許容。気になれば資金配分で分散制御


以下、詳細セクション（通常読み飛ばし可）

## 環境・コード状態
- git_sha: `<error: Command '['git', '-C', '/opt/boa` dirty=True
- config.json md5: `eb532e851a30cd2f7e69bdf0dfca3f2b`
- strategies.json md5: `1193885b4bcdeb4c8d16955d7ee412db`
- numpy=2.4.4 lightgbm=4.6.0 scipy=1.17.1
- **calibration_applied**: True ← predictor.py が校正を呼んでるか
- DB: 0.56MB / last modified 2026-04-15T07:00:02.330939+09:00

### データファイル存在確認
| file | exists | md5 | size |
|---|---|---|---|
| lgbm_model_top1.txt | True | `5b55d55bdb59df95ccfd1745d4e9b469` | 769682 |
| lgbm_model_top3.txt | True | `d5fd8d8393fd859ed913813abbf60084` | 969111 |
| calibration_v7.json | True | `1c04ab3c1a1f074da889e6f5f06adbf3` | 1450 |
| pl_corr_v8_final.json | True | `8727224dfcc3d7548845e2e41caef7be` | 1209 |

### crontab
```
# boatrace_v2 - managed by めう/Claude
SHELL=/bin/bash
PATH=/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin

# 1分毎: 統合サイクル (run_cycle.py, flock で並行実行防止)
* 8-23 * * * cd /opt/boatrace_v2 && flock -n /var/lock/run_cycle.lock /opt/boatrace/venv/bin/python3 run_cycle.py >> logs/run_cycle.log 2>&1

# 10分毎: pending alert flush
*/10 * * * * cd /opt/boatrace_v2 && /opt/boatrace/venv/bin/python3 dispatch_pending.py >> logs/dispatch.log 2>&1

# 10分毎: snapshot 生成 + GitHub 同期 (Claude 次セッション用)
*/10 * * * * cd /opt/boatrace_v2 && bash sync_snapshot_to_github.sh >> logs/sync_snapshot.log 2>&1

# 5分毎: 結果取得
*/5 * * * * cd /opt/boatrace_v2 && /opt/boatrace/venv/bin/python3 record_results.py >> logs/results.log 2>&1

# 30分毎: health check
*/30 * * * * cd /opt/boatrace_v2 && /opt/boatrace/venv/bin/python3 health.py >> logs/health.log 2>&1

# 6時: 日次総合検査
0 6 * * *  cd /opt/boatrace_v2 && /opt/boatrace/venv/bin/python3 verify_all.py >> logs/verify_all.log 2>&1

# 0時: 日次集計
5 0 * * *  cd /opt/boatrace_v2 && /opt/boatrace/venv/bin/python3 daily_summary.py >> logs/daily.log 2>&1
```

### 直近 run_cycle ログ (末尾)
```
<no log>
```

## 戦略有効/無効一覧
| id | trust | bt | ev_th | pmin | enabled |
|---|---|---|---|---|---|
| S00 | S | win | 2.5 | 0.55 | True |
| S01 | A | 2t | 5.0 | 0.6 | True |
| S02 | S | win | 5.0 | 0.1 | True |
| S03 | S | win | 5.0 | 0.2 | True |
| S04 | A | 2t | 5.0 | 0.55 | True |
| S05 | B | 3t | 10.0 | 0.4 | True |
| S06 | A | 2t | 5.0 | 0.5 | True |
| S07 | S | win | 3.0 | 0.5 | True |
| S08 | B | 3t | 10.0 | 0.5 | True |
| S09 | S | win | 2.5 | 0.55 | True |
| S10 | S | win | 2.25 | 0.6 | True |
| S11 | B | 3t | 10.0 | 0.2 | True |
| S12 | B | 3t | 10.0 | 0.4 | True |

## Webhook送信 (24h)
```
[]
```

## Phase別通知記録 (24h)
{}

## アラート件数 (24h・種類別)
```
  (なし)
```

## 戦略別 ROI (7日)
| sid | n | hits | cost | payout | PL | ROI |
|---|---|---|---|---|---|---|
| S00 | 40 | 8 | 10,400 | 3,270 | -7,130 | 0.314 |
| S01 | 7 | 0 | 2,600 | 0 | -2,600 | 0.0 |
| S02 | 129 | 8 | 28,600 | 4,530 | -24,070 | 0.158 |
| S03 | 70 | 6 | 14,800 | 2,620 | -12,180 | 0.177 |
| S04 | 9 | 0 | 3,300 | 0 | -3,300 | 0.0 |
| S05 | 8 | 0 | 1,700 | 0 | -1,700 | 0.0 |
| S06 | 12 | 0 | 3,600 | 0 | -3,600 | 0.0 |
| S07 | 42 | 6 | 10,600 | 3,700 | -6,900 | 0.349 |
| S08 | 6 | 0 | 1,200 | 0 | -1,200 | 0.0 |
| S09 | 40 | 7 | 10,400 | 2,270 | -8,130 | 0.218 |
| S10 | 26 | 6 | 6,200 | 3,920 | -2,280 | 0.632 |
| S11 | 27 | 0 | 4,300 | 0 | -4,300 | 0.0 |
| S12 | 8 | 0 | 1,700 | 0 | -1,700 | 0.0 |
| s1_3t_bomb | 5 | 1 | 500 | 14,200 | +13,700 | 28.4 |
| s2_2t_snipe | 17 | 0 | 1,700 | 0 | -1,700 | 0.0 |
| s3_3f_target | 110 | 16 | 11,000 | 7,870 | -3,130 | 0.715 |
| s4_3t_mid | 28 | 0 | 2,800 | 0 | -2,800 | 0.0 |

## 直近アラート (24h・新しい順)
```
```

## 本日残レース: 0件

## 直近送信失敗 (24h)
```
```

## 最新 predictions サンプル (計算spot-check用)
| sid | race | bt | combo | p | odds | ev | bet | at |
|---|---|---|---|---|---|---|---|---|
| S03 | 0112R | win | 2 | 0.1957 | 32.0 | 6.26 | 200 | scan=- drift=- | 20:33:34 |
| S02 | 0112R | win | 2 | 0.1957 | 32.0 | 6.26 | 200 | scan=- drift=- | 20:33:03 |
| S03 | 1511R | win | 4 | 0.1720 | 34.5 | 5.93 | 100 | scan=- drift=- | 20:00:28 |
| S02 | 1511R | win | 4 | 0.1720 | 34.5 | 5.93 | 100 | scan=- drift=- | 20:00:04 |
| S03 | 0110R | win | 6 | 0.1123 | 70.5 | 7.92 | 300 | scan=- drift=- | 19:35:09 |
| S02 | 0110R | win | 6 | 0.1123 | 70.5 | 7.92 | 300 | scan=- drift=- | 19:35:03 |
| S02 | 1510R | win | 6 | 0.0878 | 87.0 | 7.64 | 300 | scan=- drift=- | 19:31:32 |
| S07 | 1510R | win | 3 | 0.2267 | 24.7 | 5.60 | 300 | scan=- drift=- | 19:24:39 |
| S03 | 1510R | win | 3 | 0.2267 | 24.7 | 5.60 | 100 | scan=- drift=- | 19:24:34 |
| S02 | 1510R | win | 3 | 0.2267 | 24.7 | 5.60 | 100 | scan=- drift=- | 19:24:03 |

## 校正テーブル合格状況

- total: 27 グループ
- passed: 19
- failed: 8 — `2f|4, 2f|5, 3f|2, 3f|3, 3f|4, 3t|1, 3t|4, 3t|5`
- 主力グループ状態: ✅ (全12グループ合格)

---
_auto-generated by claude_snapshot.py at 2026-04-15T07:00:01.765384+09:00_