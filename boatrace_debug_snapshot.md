# ClaudeDebug スナップショット

## 🔴 現状: RED

**生成**: 2026-11-12T11:10:01.459605+09:00

### 次に取るべきアクション
> RED最優先: CRITICAL_ODDS_COLLAPSE×1 (24h) → ログ/DB確認

### 検出された問題
- 🟡 FINAL_MISSING×76 (24h)
- 🔴 PSI_DRIFT_DETECTED×34 (24h)
- 🔴 STRATEGY_CI_FAIL×16 (24h)
- 🔴 CRITICAL_ODDS_COLLAPSE×1 (24h)
- 🔴 alert_manager dispatch 失敗確定 1件（手動確認必要）

---

## 🔧 AI デバッグキュー（このClaudeが対処）

### 🟡 CODE_AUDIT_SCRAPER_FAILURE_RATE_HIGH  ×1  [2026-11-12T11:00:02]
- key: `CODE_AUDIT_SCRAPER_FAILURE_RATE_HIGH|直近 500 log行 で 3-retry 全敗 5 件 (閾値 3)`
- **FIX**: scraper 3-retry 全敗多発。boatrace.jp timeout or IP ban 疑い

### 🟡 ANOMALY_SCRAPER_FAILURE_BURST  ×5  [2026-11-12T10:51:58]
- key: `ANOMALY_SCRAPER_FAILURE_BURST|`
- **FIX**: 直近1h でscraper 3-retry 全敗多発。boatrace.jp 側timeout / IP ban / DDoS

### 🔴 PSI_DRIFT_DETECTED  ×16  [2026-11-12T10:06:49]
- key: `PSI_DRIFT_DETECTED|`
- **FIX**: ml_prob 分布の PSI>0.25→モデル入力の分布シフト。校正テーブル再生成 or モデル再学習を検討

### 🔴 STRATEGY_CI_FAIL  ×16  [2026-11-12T10:06:49]
- key: `STRATEGY_CI_FAIL|`
- **FIX**: grid戦略のOOS CI下限<1.0→論文基準で赤字リスク。strategies.json確認

### 🟡 CODE_AUDIT_SCRAPER_FAILURE_RATE_HIGH  ×1  [2026-11-12T10:00:04]
- key: `CODE_AUDIT_SCRAPER_FAILURE_RATE_HIGH|直近 500 log行 で 3-retry 全敗 4 件 (閾値 3)`
- **FIX**: scraper 3-retry 全敗多発。boatrace.jp timeout or IP ban 疑い

### 🟡 CODE_AUDIT_SCRAPER_FAILURE_RATE_HIGH  ×2  [2026-11-12T09:00:02]
- key: `CODE_AUDIT_SCRAPER_FAILURE_RATE_HIGH|直近 500 log行 で 3-retry 全敗 6 件 (閾値 3)`
- **FIX**: scraper 3-retry 全敗多発。boatrace.jp timeout or IP ban 疑い

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-11-12T06:00:27]
- key: `INSUFFICIENT_SAMPLE|S02_TETSUBAN: n=53<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-11-12T06:00:27]
- key: `INSUFFICIENT_SAMPLE|S01_NAKAANA1: n=141<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ CALIBRATION_LIVE  ×1  [2026-11-12T06:00:27]
- key: `CALIBRATION_LIVE|decile 0.15-0.20: n=8 pred=0.1878 actual=0.0000 gap=+0.1878`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-11-12T06:00:27]
- key: `ROI_STAT|S00: n=128 hit%=28.9% hit_CI[Bonf]=[18.9,41.5]% ROI=0.78 ROI_boot95=[0.55,1.04]`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-11-12T06:00:27]
- key: `INSUFFICIENT_SAMPLE|S00: n=128<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ ROI_STAT  ×1  [2026-11-12T06:00:27]
- key: `ROI_STAT|S01_NAKAANA1: n=141 hit%=30.5% hit_CI[Bonf]=[20.7,42.5]% ROI=0.74 ROI_boot95=[0.`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-11-12T06:00:27]
- key: `ROI_STAT|S02_TETSUBAN: n=53 hit%=47.2% hit_CI[Bonf]=[29.1,66.0]% ROI=1.09 ROI_boot95=[0.6`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### 🟡 ORPHAN_SCAN  ×1  [2026-11-12T06:00:27]
- key: `ORPHAN_SCAN|201 件の scan に final/retreat 追従無し`
- **FIX**: scan 後 final も retreat も無い→当該レースの final 窓が短すぎ/fetch 失敗

### ℹ️ DRIFT_BUCKET  ×1  [2026-11-12T06:00:27]
- key: `DRIFT_BUCKET|drift -30%〜-10%: n=29 hit%=27.6% ROI=0.87 (コスト 6,500/回収 5,680)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-11-12T06:00:27]
- key: `DRIFT_BUCKET|drift -10%〜+10%: n=65 hit%=49.2% ROI=1.29 (コスト 15,000/回収 19,330)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-11-12T06:00:27]
- key: `DRIFT_BUCKET|drift +10%〜+30%: n=40 hit%=25.0% ROI=0.78 (コスト 9,600/回収 7,500)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-11-12T06:00:27]
- key: `DRIFT_BUCKET|drift ≥+30%: n=31 hit%=16.1% ROI=0.48 (コスト 8,300/回収 4,010)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ CALIBRATION_LIVE  ×1  [2026-11-12T06:00:27]
- key: `CALIBRATION_LIVE|bt=win: n=322 pred=0.4739 actual=0.3261 error=+0.1478 (+31%) brier=0.2291 [OVERC`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-11-12T06:00:27]
- key: `CALIBRATION_LIVE|S00(win): n=128 pred=0.4284 hit=0.2891 cal_err=+0.1393 brier=0.2088 BSS=-0.02 RO`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用


以下、詳細セクション（通常読み飛ばし可）

## 環境・コード状態
- git_sha: `<error: Command '['git', '-C', '/opt/boa` dirty=True
- config.json md5: `eb532e851a30cd2f7e69bdf0dfca3f2b`
- strategies.json md5: `06b22dd935785e7947bf9c0f170b69a3`
- numpy=2.4.4 lightgbm=4.6.0 scipy=1.17.1
- **calibration_applied**: True ← predictor.py が校正を呼んでるか
- DB: 17.87MB / last modified 2026-11-12T11:07:18.154694+09:00

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

# 30分毎: コード/DB a
```

### 直近 run_cycle ログ (末尾)
```
08 [INFO] scraper: odds2t: 28/30 parsed
2026-11-12 11:08:05,809 [INFO] scraper: odds2f: 15/15 parsed
2026-11-12 11:08:16,821 [WARNING] scraper: fetch error (1/3): https://www.boatrace.jp/owpc/pc/race/oddstf?rno=3&jcd=17&hd=20261112: HTTPSConnectionPool(host='www.boatrace.jp', port=443): Read timed out. (read timeout=10), retry in 1s
2026-11-12 11:08:27,002 [INFO] scraper: odds_win: 2/6 parsed
2026-11-12 11:08:27,002 [INFO] scraper: fetch_race 17/3: boats=6 odds=185/191
2026-11-12 11:08:27,004 [INFO] predictor: CALIBRATION_MODE=on
2026-11-12 11:08:27,004 [INFO] predictor: combos: {'win': 2, '2t': 28, '3t': 120}
2026-11-12 11:08:27,008 [INFO] run_cycle: fetched 17/3 [scan]: 150 combos
2026-11-12 11:08:55,575 [INFO] scraper: odds3t: 120/120 parsed
2026-11-12 11:09:06,585 [WARNING] scraper: fetch error (1/3): https://www.boatrace.jp/owpc/pc/race/odds3f?rno=2&jcd=02&hd=20261112: HTTPSConnectionPool(host='www.boatrace.jp', port=443): Read timed out. (read timeout=10), retry in 1s
2026-11-12 11:09:15,767 [INFO] scraper: odds3f: 20/20 parsed
2026-11-12 11:09:26,769 [WARNING] scraper: fetch error (1/3): https://www.boatrace.jp/owpc/pc/race/odds2tf?rno=2&jcd=02&hd=20261112: HTTPSConnectionPool(host='www.boatrace.jp', port=443): Read timed out. (read timeout=10), retry in 1s
2026-11-12 11:09:35,901 [INFO] scraper: odds2t: 30/30 parsed
2026-11-12 11:09:35,902 [INFO] scraper: odds2f: 15/15 parsed
2026-11-12 11:09:44,988 [INFO] scraper: odds_win: 6/6 parsed
2026-11-12 11:09:44,989 [INFO] scraper: fetch_race 02/2: boats=6 odds=191/191
2026-11-12 11:09:44,991 [INFO] predictor: CALIBRATION_MODE=on
2026-11-12 11:09:44,991 [INFO] predictor: combos: {'win': 6, '2t': 30, '3t': 120}
2026-11-12 11:09:44,995 [INFO] run_cycle: fetched 02/2 [scan]: 156 combos
2026-11-12 11:09:56,162 [WARNING] scraper: fetch error (1/3): https://www.boatrace.jp/owpc/pc/race/racelist?rno=2&jcd=22&hd=20261112: HTTPSConnectionPool(host='www.boatrace.jp', port=443): Read timed out. (read timeout=10), retry in 1s

```

## 戦略有効/無効一覧
| id | trust | bt | ev_th | pmin | enabled |
|---|---|---|---|---|---|
| S00 | S | win | 4.0 | 0.0 | True |
| S01_NAKAANA1 | A | win | 1.5 | 0.0 | True |
| S02_TETSUBAN | A | win | 1.0 | 0.0 | True |
| S03_NAKAANA4 | B | win | 1.0 | 0.0 | False |
| S04_SELL_3T | B | 3t | 1.0 | 0.0 | False |
| S05_2T_MANKEN | B | 2t | 1.0 | 0.0 | False |
| S06_2F_AXIS1 | B | 2f | 1.0 | 0.0 | False |
| S07_2T_HONMEI | B | 2t | 1.0 | 0.0 | False |

## Webhook送信 (24h)
```
[
  {
    "target": "mirror",
    "ok": 1,
    "c": 46
  },
  {
    "target": "primary",
    "ok": 1,
    "c": 46
  }
]
```

## Phase別通知記録 (24h)
{'final': 18, 'result': 7, 'scan': 21}

## アラート件数 (24h・種類別)
```
  ANOMALY_SCRAPER_FAILURE_BURST: 237
  FINAL_MISSING: 76
  PSI_DRIFT_DETECTED: 34
  STRATEGY_CI_FAIL: 16
  ANOMALY_SCAN_FINAL_RATIO: 4
  CRITICAL_ODDS_COLLAPSE: 1
```

## 戦略別 ROI (7日)
| sid | n | hits | cost | payout | PL | ROI |
|---|---|---|---|---|---|---|
| S00 | 9 | 2 | 2,700 | 2,250 | -450 | 0.833 |
| S01_NAKAANA1 | 17 | 4 | 3,400 | 2,560 | -840 | 0.753 |
| S02_TETSUBAN | 9 | 5 | 1,800 | 1,600 | -200 | 0.889 |

## 直近アラート (24h・新しい順)
```
[11:04:22] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 5, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 510}
[11:00:09] PSI_DRIFT_DETECTED: {"bt": "win", "kind": "PSI_DRIFT_DETECTED", "n_baseline": 289, "n_recent": 33, "psi": 1.052}
[11:00:09] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 5, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 506}
[10:56:41] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 5, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 500}
[10:54:20] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 5, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 496}
[10:51:58] PSI_DRIFT_DETECTED: {"bt": "win", "kind": "PSI_DRIFT_DETECTED", "n_baseline": 289, "n_recent": 32, "psi": 1.047}
[10:51:58] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 5, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 486}
[10:41:42] FINAL_MISSING: {"deadline": "2026-11-12T09:09:00+09:00", "kind": "FINAL_MISSING", "nid": "2026111210020909", "sid": "S00"}
[10:41:42] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 472}
[10:31:15] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 461}
```

## 本日残レース: 127件

## 本日nidレジャー（ID単位完遂突合せ）
- race_schedule: 156件 登録 / 29件 締切済
- 通知発射: scan=5 nid / final=4 nid / result=1 nid
- predictions: 4 / うち結果DB記録済: 1
- ✅ 結果DBあるが通知未発射: 0件 `tools/backfill_result_notifications.py` で救済可
- 🔴 scan後final無しのまま締切: 2件（FINAL_MISSING の温床）

## 直近送信失敗 (24h)
```
```

## 最新 predictions サンプル (計算spot-check用)
| sid | race | bt | combo | p | odds | ev | bet | at |
|---|---|---|---|---|---|---|---|---|
| S01_NAKAANA1 | 236R | win | 1 | 0.4111 | 4.9 | 2.01 | 200 | scan=- drift=- | 11:07:17 |
| S00 | 236R | win | 1 | 0.4111 | 4.9 | 2.01 | 300 | scan=12.3 drift=-60.2% | 11:07:15 |
| S01_NAKAANA1 | 106R | win | 1 | 0.5476 | 3.2 | 1.75 | 200 | scan=3.5 drift=-8.6% | 10:58:12 |
| S01_NAKAANA1 | 102R | win | 1 | 0.5123 | 3.0 | 1.54 | 200 | scan=- drift=- | 09:08:37 |
| S01_NAKAANA1 | 196R | win | 1 | 0.4111 | 3.8 | 1.56 | 200 | scan=4.5 drift=-15.6% | 17:35:35 |
| S01_NAKAANA1 | 194R | win | 1 | 0.3177 | 4.0 | 1.27 | 200 | scan=- drift=- | 16:42:25 |
| S00 | 194R | win | 1 | 0.3177 | 4.0 | 1.27 | 300 | scan=10.0 drift=-60.0% | 16:42:24 |
| S01_NAKAANA1 | 243R | win | 1 | 0.3177 | 4.0 | 1.27 | 200 | scan=- drift=- | 16:20:47 |
| S00 | 192R | win | 1 | 0.5123 | 13.8 | 7.07 | 300 | scan=13.7 drift=+0.7% | 15:44:13 |
| S02_TETSUBAN | 052R | win | 1 | 0.5334 | 2.5 | 1.33 | 200 | scan=- drift=- | 10:55:37 |

## オッズドリフト統計 (7日)

| bt | n | avg | min | max | down10 | collapse(≤-30%) | any_large(≥10%) |
|---|---|---|---|---|---|---|---|
| win | 22 | -10.6% | -66.8% | +17.6% | 8 | 4 | 12 |

## 校正テーブル合格状況

- total: 27 グループ
- passed: 19
- failed: 8 — `2f|4, 2f|5, 3f|2, 3f|3, 3f|4, 3t|1, 3t|4, 3t|5`
- 主力グループ状態: ✅ (全12グループ合格)

## SRE Golden Signals (24h)

| Signal | Value |
|---|---|
| **Latency** (scan→final avg) | 435.6s |
| **Latency** (scan→final max) | 635.1s |
| **Traffic** (notifications 24h) | 46 |
| **Errors** (send fail rate) | ✅ 0.0% |
| **Saturation** (S00) | 300円 used |
| **Saturation** (S01_NAKAANA1) | 600円 used |

## 信ぴょう性メトリクス（予測精度の証拠）

### bt別: 予測確率 vs 実的中率
| bt | n | 予測avg | 実的中率 | 校正誤差 | 過信度 | Brier |
|---|---|---|---|---|---|---|
| win | 321 | 0.4738 | 0.3240 | +0.1499 | 🟡+32% | 0.2295 |

### 戦略別: 校正精度 + Brier Skill Score
| sid | bt | n | pred | actual | Brier | BSS | ROI |
|---|---|---|---|---|---|---|---|
| S00 | win | 128 | 0.4284 | 0.2891 | 0.2088 | 🔴-0.02 | 0.784 |
| S01_NAKAANA1 | win | 140 | 0.4857 | 0.3000 | 0.2367 | 🔴-0.13 | 0.735 |
| S02_TETSUBAN | win | 53 | 0.5522 | 0.4717 | 0.2606 | 🔴-0.05 | 1.089 |

### 確率デシル別: 校正カーブ
| 確率帯 | n | 予測avg | 実的中率 | gap |
|---|---|---|---|---|
| 0.15-0.20 | 8 | 0.1878 | 0.0000 | 🔴+0.1878 |
| 0.20-0.30 | 7 | 0.2290 | 0.1429 | 🔴+0.0862 |
| 0.30-0.50 | 120 | 0.4141 | 0.2917 | 🔴+0.1224 |
| 0.50+ | 182 | 0.5438 | 0.3736 | 🔴+0.1701 |

## Settlement Ratio データ品質

- 学習済み: 4バンド / fallback: 13バンド
| bt | odds帯 | source | n | ratio |
|---|---|---|---|---|
| win | <3.0 | ✅learned | 203 | 0.805 |
| win | <5.0 | ✅learned | 370 | 0.741 |
| win | <10.0 | ✅learned | 157 | 0.451 |
| win | <20.0 | ✅learned | 48 | 0.252 |
| win | <50.0 | ⚠️fallback | 8 | 0.1 |
| win | ∞ | ⚠️fallback | 0 | 0.1 |
| 2t | <10.0 | ⚠️fallback | 0 | 0.5 |
| 2t | <30.0 | ⚠️fallback | 0 | 0.35 |
| 2t | ∞ | ⚠️fallback | 0 | 0.25 |
| 3t | <10.0 | ⚠️fallback | 1 | 0.4 |
| 3t | <50.0 | ⚠️fallback | 0 | 0.4 |
| 3t | <200.0 | ⚠️fallback | 0 | 0.3 |
| 3t | ∞ | ⚠️fallback | 0 | 0.2 |
| 2f | <10.0 | ⚠️fallback | 0 | 0.45 |
| 2f | ∞ | ⚠️fallback | 0 | 0.3 |
| 3f | <50.0 | ⚠️fallback | 0 | 0.4 |
| 3f | ∞ | ⚠️fallback | 0 | 0.25 |

---
_auto-generated by claude_snapshot.py at 2026-11-12T11:10:01.459605+09:00_