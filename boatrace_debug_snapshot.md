# ClaudeDebug スナップショット

## 🔴 現状: RED

**生成**: 2026-04-16T03:20:01.137939+09:00

### 次に取るべきアクション
> RED最優先: CRITICAL_ODDS_COLLAPSE×2 (24h) → ログ/DB確認

### 検出された問題
- 🟡 LARGE_ODDS_DRIFT×11 (24h)
- 🔴 CRITICAL_ODDS_COLLAPSE×2 (24h)

---

## 🔧 AI デバッグキュー（このClaudeが対処）

### 🟡 HEALTH_CHECK_FAIL  ×2  [2026-04-16T02:30:01]
- key: `HEALTH_CHECK_FAIL`
- **FIX**: health.py の check 失敗→対応する check 名から該当テーブル/指標を確認

### ℹ️ ROI_STAT  ×2  [2026-04-15T15:17:09]
- key: `ROI_STAT|S11: n=32 hit%=0.0% hit_CI[Bonf]=[0.0,20.7]% ROI=0.00 ROI_boot95=[0.00,0.00]`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ INSUFFICIENT_SAMPLE  ×2  [2026-04-15T15:17:09]
- key: `INSUFFICIENT_SAMPLE|S11: n=32<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ ROI_STAT  ×2  [2026-04-15T15:17:09]
- key: `ROI_STAT|S02: n=137 hit%=10.2% hit_CI[Bonf]=[4.9,20.1]% ROI=0.23 ROI_boot95=[0.14,0.52]`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ INSUFFICIENT_SAMPLE  ×2  [2026-04-15T15:17:09]
- key: `INSUFFICIENT_SAMPLE|S02: n=137<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### 🟡 ORPHAN_SCAN  ×2  [2026-04-15T15:17:09]
- key: `ORPHAN_SCAN|3 件の scan に final/retreat 追従無し`
- **FIX**: scan 後 final も retreat も無い→当該レースの final 窓が短すぎ/fetch 失敗

### 🔴 STRATEGY_COLLAPSE  ×3  [2026-04-15T14:50:46]
- key: `STRATEGY_COLLAPSE|2026-04-13 017R combo=1 を 4 戦略が同時採用 → 分散効果ゼロ`
- **FIX**: 4戦略以上が同 combo を採用。v18 仕様的には許容。気になれば資金配分で分散制御

### 🔴 STRATEGY_COLLAPSE  ×3  [2026-04-15T14:50:46]
- key: `STRATEGY_COLLAPSE|2026-04-14 024R combo=1 を 6 戦略が同時採用 → 分散効果ゼロ`
- **FIX**: 4戦略以上が同 combo を採用。v18 仕様的には許容。気になれば資金配分で分散制御

### 🔴 STRATEGY_COLLAPSE  ×3  [2026-04-15T14:50:46]
- key: `STRATEGY_COLLAPSE|2026-04-14 029R combo=1 を 6 戦略が同時採用 → 分散効果ゼロ`
- **FIX**: 4戦略以上が同 combo を採用。v18 仕様的には許容。気になれば資金配分で分散制御

### 🔴 STRATEGY_COLLAPSE  ×3  [2026-04-15T14:50:46]
- key: `STRATEGY_COLLAPSE|2026-04-12 0411R combo=1 を 4 戦略が同時採用 → 分散効果ゼロ`
- **FIX**: 4戦略以上が同 combo を採用。v18 仕様的には許容。気になれば資金配分で分散制御

### 🔴 STRATEGY_COLLAPSE  ×3  [2026-04-15T14:50:46]
- key: `STRATEGY_COLLAPSE|2026-04-11 069R combo=1-5-4 を 4 戦略が同時採用 → 分散効果ゼロ`
- **FIX**: 4戦略以上が同 combo を採用。v18 仕様的には許容。気になれば資金配分で分散制御

### 🔴 STRATEGY_COLLAPSE  ×3  [2026-04-15T14:50:46]
- key: `STRATEGY_COLLAPSE|2026-04-12 066R combo=1-4-2 を 4 戦略が同時採用 → 分散効果ゼロ`
- **FIX**: 4戦略以上が同 combo を採用。v18 仕様的には許容。気になれば資金配分で分散制御

### 🔴 STRATEGY_COLLAPSE  ×3  [2026-04-15T14:50:46]
- key: `STRATEGY_COLLAPSE|2026-04-14 103R combo=1 を 5 戦略が同時採用 → 分散効果ゼロ`
- **FIX**: 4戦略以上が同 combo を採用。v18 仕様的には許容。気になれば資金配分で分散制御

### 🔴 STRATEGY_COLLAPSE  ×3  [2026-04-15T14:50:46]
- key: `STRATEGY_COLLAPSE|2026-04-11 119R combo=1 を 5 戦略が同時採用 → 分散効果ゼロ`
- **FIX**: 4戦略以上が同 combo を採用。v18 仕様的には許容。気になれば資金配分で分散制御

### 🔴 STRATEGY_COLLAPSE  ×3  [2026-04-15T14:50:46]
- key: `STRATEGY_COLLAPSE|20260410 117R combo=1-4-3 を 4 戦略が同時採用 → 分散効果ゼロ`
- **FIX**: 4戦略以上が同 combo を採用。v18 仕様的には許容。気になれば資金配分で分散制御

### 🔴 STRATEGY_COLLAPSE  ×3  [2026-04-15T14:50:46]
- key: `STRATEGY_COLLAPSE|2026-04-11 144R combo=1 を 4 戦略が同時採用 → 分散効果ゼロ`
- **FIX**: 4戦略以上が同 combo を採用。v18 仕様的には許容。気になれば資金配分で分散制御

### 🔴 STRATEGY_COLLAPSE  ×3  [2026-04-15T14:50:46]
- key: `STRATEGY_COLLAPSE|2026-04-11 1410R combo=1 を 4 戦略が同時採用 → 分散効果ゼロ`
- **FIX**: 4戦略以上が同 combo を採用。v18 仕様的には許容。気になれば資金配分で分散制御

### 🔴 STRATEGY_COLLAPSE  ×3  [2026-04-15T14:50:46]
- key: `STRATEGY_COLLAPSE|2026-04-12 145R combo=1 を 4 戦略が同時採用 → 分散効果ゼロ`
- **FIX**: 4戦略以上が同 combo を採用。v18 仕様的には許容。気になれば資金配分で分散制御

### 🔴 STRATEGY_COLLAPSE  ×3  [2026-04-15T14:50:46]
- key: `STRATEGY_COLLAPSE|2026-04-12 148R combo=1 を 6 戦略が同時採用 → 分散効果ゼロ`
- **FIX**: 4戦略以上が同 combo を採用。v18 仕様的には許容。気になれば資金配分で分散制御

### 🔴 STRATEGY_COLLAPSE  ×3  [2026-04-15T14:50:46]
- key: `STRATEGY_COLLAPSE|2026-04-13 147R combo=1 を 5 戦略が同時採用 → 分散効果ゼロ`
- **FIX**: 4戦略以上が同 combo を採用。v18 仕様的には許容。気になれば資金配分で分散制御


以下、詳細セクション（通常読み飛ばし可）

## 環境・コード状態
- git_sha: `<error: Command '['git', '-C', '/opt/boa` dirty=True
- config.json md5: `eb532e851a30cd2f7e69bdf0dfca3f2b`
- strategies.json md5: `4188887370d24d5615d79ab97a20c75c`
- numpy=2.4.4 lightgbm=4.6.0 scipy=1.17.1
- **calibration_applied**: True ← predictor.py が校正を呼んでるか
- DB: 0.99MB / last modified 2026-04-16T03:00:02.681066+09:00

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
0 3 * * * find /opt -maxdepth 1 -name "boatrace_v2.bak_*" -mtime +7 -exec rm -rf {} \; # backup cleanup
```

### 直近 run_cycle ログ (末尾)
```
 159
    形式: 🎯 **世界観セリフっ…！** 実データ（ROI/n）+ 行動指針
        ^
SyntaxError: invalid character '🎯' (U+1F3AF)
  File "/opt/boatrace_v2/run_cycle.py", line 159
    形式: 🎯 **世界観セリフっ…！** 実データ（ROI/n）+ 行動指針
        ^
SyntaxError: invalid character '🎯' (U+1F3AF)
  File "/opt/boatrace_v2/run_cycle.py", line 159
    形式: 🎯 **世界観セリフっ…！** 実データ（ROI/n）+ 行動指針
        ^
SyntaxError: invalid character '🎯' (U+1F3AF)
  File "/opt/boatrace_v2/run_cycle.py", line 159
    形式: 🎯 **世界観セリフっ…！** 実データ（ROI/n）+ 行動指針
        ^
SyntaxError: invalid character '🎯' (U+1F3AF)
  File "/opt/boatrace_v2/run_cycle.py", line 159
    形式: 🎯 **世界観セリフっ…！** 実データ（ROI/n）+ 行動指針
        ^
SyntaxError: invalid character '🎯' (U+1F3AF)
  File "/opt/boatrace_v2/run_cycle.py", line 159
    形式: 🎯 **世界観セリフっ…！** 実データ（ROI/n）+ 行動指針
        ^
SyntaxError: invalid character '🎯' (U+1F3AF)
  File "/opt/boatrace_v2/run_cycle.py", line 159
    形式: 🎯 **世界観セリフっ…！** 実データ（ROI/n）+ 行動指針
        ^
SyntaxError: invalid character '🎯' (U+1F3AF)
  File "/opt/boatrace_v2/run_cycle.py", line 159
    形式: 🎯 **世界観セリフっ…！** 実データ（ROI/n）+ 行動指針
        ^
SyntaxError: invalid character '🎯' (U+1F3AF)
  File "/opt/boatrace_v2/run_cycle.py", line 159
    形式: 🎯 **世界観セリフっ…！** 実データ（ROI/n）+ 行動指針
        ^
SyntaxError: invalid character '🎯' (U+1F3AF)
  File "/opt/boatrace_v2/run_cycle.py", line 159
    形式: 🎯 **世界観セリフっ…！** 実データ（ROI/n）+ 行動指針
        ^
SyntaxError: invalid character '🎯' (U+1F3AF)
  File "/opt/boatrace_v2/run_cycle.py", line 159
    形式: 🎯 **世界観セリフっ…！** 実データ（ROI/n）+ 行動指針
        ^
SyntaxError: invalid character '🎯' (U+1F3AF)
  File "/opt/boatrace_v2/run_cycle.py", line 159
    形式: 🎯 **世界観セリフっ…！** 実データ（ROI/n）+ 行動指針
        ^
SyntaxError: invalid character '🎯' (U+1F3AF)
  File "/opt/boatrace_v2/run_cycle.py", line 159
    形式: 🎯 **世界観セリフっ…！** 実データ（ROI/n）+ 行動指針
        ^
SyntaxError: invalid character '🎯' (U+1F3AF)
  File "/opt/boatrace_v2/run_cycle.py", line 159
    形式: 🎯 **世界観セリフっ…！** 実データ（ROI/n）+ 行動指針
        ^
SyntaxError: invalid character '🎯' (U+1F3AF)

```

## 戦略有効/無効一覧
| id | trust | bt | ev_th | pmin | enabled |
|---|---|---|---|---|---|
| S00 | S | win | 2.25 | 0.6 | True |
| S01 | A | 2t | 5.0 | 0.6 | False |
| S02 | S | win | 5.0 | 0.1 | True |
| S03 | S | win | 5.0 | 0.2 | True |
| S04 | A | 2t | 5.0 | 0.55 | False |
| S05 | B | 3t | 10.0 | 0.4 | False |
| S06 | A | 2t | 5.0 | 0.5 | False |
| S07 | S | win | 3.0 | 0.5 | True |
| S08 | B | 3t | 10.0 | 0.5 | False |
| S09 | S | win | 2.5 | 0.55 | True |
| S10 | S | win | 2.5 | 0.55 | True |
| S11 | B | 3t | 10.0 | 0.2 | False |
| S12 | B | 3t | 10.0 | 0.4 | False |
| S_EXACTA_MID | A | 2t | 3.0 | 0.3 | True |
| S_EXACTA_HI | A | 2t | 4.0 | 0.3 | True |
| S_STABLE | A | 2f | 2.0 | 0.0 | True |

## Webhook送信 (24h)
```
[
  {
    "target": "mirror",
    "ok": 1,
    "c": 173
  },
  {
    "target": "primary",
    "ok": 1,
    "c": 173
  }
]
```

## Phase別通知記録 (24h)
{'final': 88, 'scan': 85}

## アラート件数 (24h・種類別)
```
  LARGE_ODDS_DRIFT: 11
  CRITICAL_ODDS_COLLAPSE: 2
```

## 戦略別 ROI (7日)
| sid | n | hits | cost | payout | PL | ROI |
|---|---|---|---|---|---|---|
| S00 | 42 | 19 | 11,000 | 10,420 | -580 | 0.947 |
| S01 | 8 | 0 | 2,800 | 0 | -2,800 | 0.0 |
| S02 | 137 | 14 | 31,000 | 7,000 | -24,000 | 0.226 |
| S03 | 75 | 12 | 16,300 | 5,090 | -11,210 | 0.312 |
| S04 | 12 | 0 | 3,900 | 0 | -3,900 | 0.0 |
| S05 | 10 | 0 | 1,900 | 0 | -1,900 | 0.0 |
| S06 | 15 | 0 | 4,200 | 0 | -4,200 | 0.0 |
| S07 | 44 | 17 | 11,200 | 8,860 | -2,340 | 0.791 |
| S08 | 8 | 0 | 1,400 | 0 | -1,400 | 0.0 |
| S09 | 42 | 19 | 11,000 | 10,420 | -580 | 0.947 |
| S10 | 27 | 15 | 6,500 | 7,420 | +920 | 1.142 |
| S11 | 32 | 0 | 4,800 | 0 | -4,800 | 0.0 |
| S12 | 10 | 0 | 1,900 | 0 | -1,900 | 0.0 |

## 直近アラート (24h・新しい順)
```
[14:45:36] LARGE_ODDS_DRIFT: {"kind": "LARGE_ODDS_DRIFT", "sid": "S09", "race": "029R", "combo": "1", "scan": 6.5, "final": 7.6, "drift_pct": 16.9}
[14:45:36] LARGE_ODDS_DRIFT: {"kind": "LARGE_ODDS_DRIFT", "sid": "S07", "race": "029R", "combo": "1", "scan": 6.5, "final": 7.6, "drift_pct": 16.9}
[14:45:36] LARGE_ODDS_DRIFT: {"kind": "LARGE_ODDS_DRIFT", "sid": "S00", "race": "029R", "combo": "1", "scan": 6.5, "final": 7.6, "drift_pct": 16.9}
[12:03:27] LARGE_ODDS_DRIFT: {"kind": "LARGE_ODDS_DRIFT", "sid": "S12", "race": "174R", "combo": "1-6-5", "scan": 707.5, "final": 628.3, "drift_pct": -11.2}
[12:03:27] LARGE_ODDS_DRIFT: {"kind": "LARGE_ODDS_DRIFT", "sid": "S12", "race": "174R", "combo": "1-6-3", "scan": 501.1, "final": 672.6, "drift_pct": 34.2}
[12:03:27] LARGE_ODDS_DRIFT: {"kind": "LARGE_ODDS_DRIFT", "sid": "S11", "race": "174R", "combo": "1-6-5", "scan": 707.5, "final": 628.3, "drift_pct": -11.2}
[12:03:27] LARGE_ODDS_DRIFT: {"kind": "LARGE_ODDS_DRIFT", "sid": "S11", "race": "174R", "combo": "1-6-3", "scan": 501.1, "final": 672.6, "drift_pct": 34.2}
[12:03:27] LARGE_ODDS_DRIFT: {"kind": "LARGE_ODDS_DRIFT", "sid": "S08", "race": "174R", "combo": "1-6-5", "scan": 707.5, "final": 628.3, "drift_pct": -11.2}
[12:03:27] LARGE_ODDS_DRIFT: {"kind": "LARGE_ODDS_DRIFT", "sid": "S08", "race": "174R", "combo": "1-6-3", "scan": 501.1, "final": 672.6, "drift_pct": 34.2}
[12:03:27] LARGE_ODDS_DRIFT: {"kind": "LARGE_ODDS_DRIFT", "sid": "S05", "race": "174R", "combo": "1-6-5", "scan": 707.5, "final": 628.3, "drift_pct": -11.2}
```

## 本日残レース: 144件

## 直近送信失敗 (24h)
```
```

## 最新 predictions サンプル (計算spot-check用)
| sid | race | bt | combo | p | odds | ev | bet | at |
|---|---|---|---|---|---|---|---|---|
| S02 | 201R | win | 4 | 0.1360 | 76.5 | 10.40 | 300 | scan=73.1 drift=+4.7% | 15:16:21 |
| S02 | 201R | win | 3 | 0.1161 | 153.0 | 17.77 | 300 | scan=- drift=- | 15:16:21 |
| S09 | 029R | win | 1 | 0.5650 | 7.6 | 4.29 | 300 | scan=6.5 drift=+16.9% | 14:45:35 |
| S07 | 029R | win | 1 | 0.5650 | 7.6 | 4.29 | 300 | scan=6.5 drift=+16.9% | 14:45:34 |
| S00 | 029R | win | 1 | 0.5650 | 7.6 | 4.29 | 300 | scan=6.5 drift=+16.9% | 14:45:34 |
| S03 | 178R | win | 2 | 0.2118 | 31.8 | 6.73 | 300 | scan=30.0 drift=+6.0% | 14:04:24 |
| S02 | 178R | win | 2 | 0.2118 | 31.8 | 6.73 | 300 | scan=30.0 drift=+6.0% | 14:04:22 |
| S11 | 167R | 3t | 4-1-3 | 0.0357 | 312.5 | 11.17 | 100 | scan=- drift=- | 13:52:34 |
| S06 | 167R | 2t | 1-4 | 0.1341 | 66.9 | 8.97 | 200 | scan=71.5 drift=-6.4% | 13:52:33 |
| S04 | 167R | 2t | 1-4 | 0.1341 | 66.9 | 8.97 | 200 | scan=71.5 drift=-6.4% | 13:52:31 |

## オッズドリフト統計 (7日)

| bt | n | avg | min | max | down10 | collapse(≤-30%) | any_large(≥10%) |
|---|---|---|---|---|---|---|---|
| 2t | 5 | -7.5% | -9.0% | -6.4% | 0 | 0 | 0 |
| 3t | 10 | +10.2% | -11.2% | +34.2% | 4 | 0 | 8 |
| win | 14 | -0.2% | -64.6% | +16.9% | 2 | 2 | 5 |

## 校正テーブル合格状況

- total: 27 グループ
- passed: 19
- failed: 8 — `2f|4, 2f|5, 3f|2, 3f|3, 3f|4, 3t|1, 3t|4, 3t|5`
- 主力グループ状態: ✅ (全12グループ合格)

---
_auto-generated by claude_snapshot.py at 2026-04-16T03:20:01.137939+09:00_