# ClaudeDebug スナップショット

## 🔴 現状: RED

**生成**: 2026-11-05T12:40:01.287282+09:00

### 次に取るべきアクション
> RED最優先: PSI_DRIFT_DETECTED×26 (24h) → ログ/DB確認

### 検出された問題
- 🟡 FINAL_MISSING×87 (24h)
- 🔴 PSI_DRIFT_DETECTED×26 (24h)
- 🔴 STRATEGY_CI_FAIL×17 (24h)
- 🔴 CALIBRATION_DRIFT×12 (24h)
- 🔴 alert_manager dispatch 失敗確定 1件（手動確認必要）

---

## 🔧 AI デバッグキュー（このClaudeが対処）

### 🟡 ANOMALY_SCRAPER_FAILURE_BURST  ×2  [2026-11-05T12:31:20]
- key: `ANOMALY_SCRAPER_FAILURE_BURST|`
- **FIX**: 直近1h でscraper 3-retry 全敗多発。boatrace.jp 側timeout / IP ban / DDoS

### 🟡 CODE_AUDIT_SCRAPER_FAILURE_RATE_HIGH  ×1  [2026-11-05T12:30:02]
- key: `CODE_AUDIT_SCRAPER_FAILURE_RATE_HIGH|直近 500 log行 で 3-retry 全敗 8 件 (閾値 3)`
- **FIX**: scraper 3-retry 全敗多発。boatrace.jp timeout or IP ban 疑い

### 🔴 PSI_DRIFT_DETECTED  ×7  [2026-11-05T12:15:04]
- key: `PSI_DRIFT_DETECTED|`
- **FIX**: ml_prob 分布の PSI>0.25→モデル入力の分布シフト。校正テーブル再生成 or モデル再学習を検討

### 🔴 STRATEGY_CI_FAIL  ×7  [2026-11-05T12:15:04]
- key: `STRATEGY_CI_FAIL|`
- **FIX**: grid戦略のOOS CI下限<1.0→論文基準で赤字リスク。strategies.json確認

### 🟡 CODE_AUDIT_SCRAPER_FAILURE_RATE_HIGH  ×1  [2026-11-05T12:00:02]
- key: `CODE_AUDIT_SCRAPER_FAILURE_RATE_HIGH|直近 500 log行 で 3-retry 全敗 10 件 (閾値 3)`
- **FIX**: scraper 3-retry 全敗多発。boatrace.jp timeout or IP ban 疑い

### 🟡 ANOMALY_SCAN_FINAL_RATIO  ×3  [2026-11-05T11:31:11]
- key: `ANOMALY_SCAN_FINAL_RATIO|`
- **FIX**: scan→final成立率が7日baselineから2σ逸脱。scan/final window設定・odds取得タイミング

### 🟡 CODE_AUDIT_SCRAPER_FAILURE_RATE_HIGH  ×1  [2026-11-05T11:30:04]
- key: `CODE_AUDIT_SCRAPER_FAILURE_RATE_HIGH|直近 500 log行 で 3-retry 全敗 9 件 (閾値 3)`
- **FIX**: scraper 3-retry 全敗多発。boatrace.jp timeout or IP ban 疑い

### 🟡 CODE_AUDIT_SCRAPER_FAILURE_RATE_HIGH  ×1  [2026-11-05T11:00:03]
- key: `CODE_AUDIT_SCRAPER_FAILURE_RATE_HIGH|直近 500 log行 で 3-retry 全敗 7 件 (閾値 3)`
- **FIX**: scraper 3-retry 全敗多発。boatrace.jp timeout or IP ban 疑い

### 🟡 CODE_AUDIT_SCRAPER_FAILURE_RATE_HIGH  ×2  [2026-11-05T09:30:02]
- key: `CODE_AUDIT_SCRAPER_FAILURE_RATE_HIGH|直近 500 log行 で 3-retry 全敗 4 件 (閾値 3)`
- **FIX**: scraper 3-retry 全敗多発。boatrace.jp timeout or IP ban 疑い

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-11-05T06:00:45]
- key: `INSUFFICIENT_SAMPLE|S00: n=158<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-11-05T06:00:45]
- key: `INSUFFICIENT_SAMPLE|S01_NAKAANA1: n=164<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-11-05T06:00:45]
- key: `INSUFFICIENT_SAMPLE|S02_TETSUBAN: n=64<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### 🟡 ORPHAN_SCAN  ×1  [2026-11-05T06:00:45]
- key: `ORPHAN_SCAN|178 件の scan に final/retreat 追従無し`
- **FIX**: scan 後 final も retreat も無い→当該レースの final 窓が短すぎ/fetch 失敗

### ℹ️ CALIBRATION_LIVE  ×1  [2026-11-05T06:00:45]
- key: `CALIBRATION_LIVE|decile 0.20-0.30: n=9 pred=0.2290 actual=0.1111 gap=+0.1179`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ DRIFT_BUCKET  ×1  [2026-11-05T06:00:45]
- key: `DRIFT_BUCKET|drift +10%〜+30%: n=53 hit%=28.3% ROI=0.81 (コスト 12,800/回収 10,400)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ CALIBRATION_LIVE  ×1  [2026-11-05T06:00:45]
- key: `CALIBRATION_LIVE|decile 0.15-0.20: n=8 pred=0.1878 actual=0.0000 gap=+0.1878`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-11-05T06:00:45]
- key: `ROI_STAT|S00: n=158 hit%=29.1% hit_CI[Bonf]=[19.9,40.4]% ROI=0.78 ROI_boot95=[0.58,1.01]`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-11-05T06:00:45]
- key: `ROI_STAT|S01_NAKAANA1: n=164 hit%=32.9% hit_CI[Bonf]=[23.4,44.1]% ROI=0.77 ROI_boot95=[0.`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-11-05T06:00:45]
- key: `ROI_STAT|S02_TETSUBAN: n=64 hit%=45.3% hit_CI[Bonf]=[28.9,62.8]% ROI=1.05 ROI_boot95=[0.6`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ DRIFT_BUCKET  ×1  [2026-11-05T06:00:45]
- key: `DRIFT_BUCKET|drift -30%〜-10%: n=34 hit%=38.2% ROI=1.02 (コスト 7,700/回収 7,860)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料


以下、詳細セクション（通常読み飛ばし可）

## 環境・コード状態
- git_sha: `<error: Command '['git', '-C', '/opt/boa` dirty=True
- config.json md5: `eb532e851a30cd2f7e69bdf0dfca3f2b`
- strategies.json md5: `06b22dd935785e7947bf9c0f170b69a3`
- numpy=2.4.4 lightgbm=4.6.0 scipy=1.17.1
- **calibration_applied**: True ← predictor.py が校正を呼んでるか
- DB: 17.58MB / last modified 2026-11-05T12:36:48.122462+09:00

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
6-11-05 12:38:10,329 [INFO] predictor: combos: {'win': 3, '2t': 30, '3t': 120}
2026-11-05 12:38:10,333 [INFO] run_cycle: fetched 17/6 [final]: 153 combos
2026-11-05 12:38:21,441 [WARNING] scraper: fetch error (1/3): https://www.boatrace.jp/owpc/pc/race/racelist?rno=5&jcd=03&hd=20261105: HTTPSConnectionPool(host='www.boatrace.jp', port=443): Read timed out. (read timeout=10), retry in 1s
2026-11-05 12:38:50,887 [INFO] scraper: odds3t: 120/120 parsed
2026-11-05 12:38:59,963 [INFO] scraper: odds3f: 20/20 parsed
2026-11-05 12:39:09,087 [INFO] scraper: odds2t: 30/30 parsed
2026-11-05 12:39:09,089 [INFO] scraper: odds2f: 15/15 parsed
2026-11-05 12:39:20,100 [WARNING] scraper: fetch error (1/3): https://www.boatrace.jp/owpc/pc/race/oddstf?rno=5&jcd=03&hd=20261105: HTTPSConnectionPool(host='www.boatrace.jp', port=443): Read timed out. (read timeout=10), retry in 1s
2026-11-05 12:39:31,134 [WARNING] scraper: fetch error (2/3): https://www.boatrace.jp/owpc/pc/race/oddstf?rno=5&jcd=03&hd=20261105: HTTPSConnectionPool(host='www.boatrace.jp', port=443): Read timed out. (read timeout=10), retry in 3s
2026-11-05 12:39:44,178 [WARNING] scraper: fetch error (3/3): https://www.boatrace.jp/owpc/pc/race/oddstf?rno=5&jcd=03&hd=20261105: HTTPSConnectionPool(host='www.boatrace.jp', port=443): Read timed out. (read timeout=10), retry in 9s
2026-11-05 12:39:44,178 [ERROR] scraper: fetch failed after 3 retries: https://www.boatrace.jp/owpc/pc/race/oddstf?rno=5&jcd=03&hd=20261105
2026-11-05 12:39:44,178 [INFO] scraper: fetch_race 03/5: boats=6 odds=185/191
2026-11-05 12:39:44,180 [INFO] predictor: CALIBRATION_MODE=on
2026-11-05 12:39:44,180 [INFO] predictor: combos: {'2t': 30, '3t': 120}
2026-11-05 12:39:44,184 [INFO] run_cycle: fetched 03/5 [scan]: 150 combos
2026-11-05 12:39:55,350 [WARNING] scraper: fetch error (1/3): https://www.boatrace.jp/owpc/pc/race/racelist?rno=5&jcd=04&hd=20261105: HTTPSConnectionPool(host='www.boatrace.jp', port=443): Read timed out. (read timeout=10), retry in 1s

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
    "c": 43
  },
  {
    "target": "primary",
    "ok": 1,
    "c": 43
  }
]
```

## Phase別通知記録 (24h)
{'final': 15, 'result': 7, 'scan': 21}

## アラート件数 (24h・種類別)
```
  ANOMALY_SCRAPER_FAILURE_BURST: 260
  FINAL_MISSING: 87
  PSI_DRIFT_DETECTED: 26
  CIRCUIT_BREAKER_NO_ACTION: 22
  STRATEGY_CI_FAIL: 17
  CALIBRATION_DRIFT: 12
  ANOMALY_SCAN_FINAL_RATIO: 2
```

## 戦略別 ROI (7日)
| sid | n | hits | cost | payout | PL | ROI |
|---|---|---|---|---|---|---|
| S00 | 15 | 2 | 4,500 | 2,130 | -2,370 | 0.473 |
| S01_NAKAANA1 | 19 | 8 | 3,800 | 3,960 | +160 | 1.042 |
| S02_TETSUBAN | 8 | 1 | 1,600 | 220 | -1,380 | 0.138 |

## 直近アラート (24h・新しい順)
```
[12:36:48] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 10, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 492}
[12:31:20] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 9, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 490}
[12:25:04] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 8, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 506}
[12:24:22] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 8, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 510}
[12:19:03] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 8, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 520}
[12:18:34] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 9, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 518}
[12:15:04] STRATEGY_CI_FAIL: {"ci_lo": null, "kind": "STRATEGY_CI_FAIL", "sid": "S02_TETSUBAN"}
[12:15:04] PSI_DRIFT_DETECTED: {"bt": "win", "kind": "PSI_DRIFT_DETECTED", "n_baseline": 343, "n_recent": 42, "psi": 0.48}
[12:15:04] FINAL_MISSING: {"deadline": "2026-11-05T11:44:00+09:00", "kind": "FINAL_MISSING", "nid": "2026110522031144", "sid": "S00"}
[12:15:04] FINAL_MISSING: {"deadline": "2026-11-05T11:42:00+09:00", "kind": "FINAL_MISSING", "nid": "2026110517041142", "sid": "S00"}
```

## 本日残レース: 93件

## 本日nidレジャー（ID単位完遂突合せ）
- race_schedule: 144件 登録 / 51件 締切済
- 通知発射: scan=6 nid / final=4 nid / result=1 nid
- predictions: 1 / うち結果DB記録済: 1
- ✅ 結果DBあるが通知未発射: 0件 `tools/backfill_result_notifications.py` で救済可
- 🔴 scan後final無しのまま締切: 5件（FINAL_MISSING の温床）

## 直近送信失敗 (24h)
```
```

## 最新 predictions サンプル (計算spot-check用)
| sid | race | bt | combo | p | odds | ev | bet | at |
|---|---|---|---|---|---|---|---|---|
| S02_TETSUBAN | 214R | win | 1 | 0.5476 | 2.3 | 1.26 | 200 | scan=- drift=- | 09:52:27 |
| S01_NAKAANA1 | 197R | win | 1 | 0.4994 | 3.4 | 1.70 | 200 | scan=3.5 drift=-2.9% | 20:23:15 |
| S01_NAKAANA1 | 194R | win | 1 | 0.4989 | 3.8 | 1.90 | 200 | scan=4.6 drift=-17.4% | 19:01:10 |
| S00 | 153R | win | 1 | 0.5334 | 5.1 | 2.72 | 300 | scan=- drift=- | 16:17:14 |
| S00 | 2210R | win | 1 | 0.0568 | 11.0 | 0.62 | 300 | scan=- drift=- | 15:11:42 |
| S01_NAKAANA1 | 097R | win | 1 | 0.4111 | 3.2 | 1.32 | 200 | scan=3.5 drift=-8.6% | 13:21:49 |
| S02_TETSUBAN | 2110R | win | 1 | 0.4111 | 2.7 | 1.11 | 200 | scan=- drift=- | 13:03:25 |
| S02_TETSUBAN | 092R | win | 1 | 0.5123 | 2.0 | 1.02 | 200 | scan=- drift=- | 10:55:26 |
| S02_TETSUBAN | 212R | win | 1 | 0.5735 | 2.4 | 1.38 | 200 | scan=- drift=- | 08:59:15 |
| S01_NAKAANA1 | 191R | win | 1 | 0.4989 | 3.1 | 1.55 | 200 | scan=3.5 drift=-11.4% | 17:40:03 |

## オッズドリフト統計 (7日)

| bt | n | avg | min | max | down10 | collapse(≤-30%) | any_large(≥10%) |
|---|---|---|---|---|---|---|---|
| win | 18 | -6.4% | -54.4% | +54.8% | 6 | 3 | 10 |

## 校正テーブル合格状況

- total: 27 グループ
- passed: 19
- failed: 8 — `2f|4, 2f|5, 3f|2, 3f|3, 3f|4, 3t|1, 3t|4, 3t|5`
- 主力グループ状態: ✅ (全12グループ合格)

## SRE Golden Signals (24h)

| Signal | Value |
|---|---|
| **Latency** (scan→final avg) | 436.0s |
| **Latency** (scan→final max) | 671.3s |
| **Traffic** (notifications 24h) | 43 |
| **Errors** (send fail rate) | ✅ 0.0% |
| **Saturation** (S02_TETSUBAN) | 200円 used |

## 信ぴょう性メトリクス（予測精度の証拠）

### bt別: 予測確率 vs 実的中率
| bt | n | 予測avg | 実的中率 | 校正誤差 | 過信度 | Brier |
|---|---|---|---|---|---|---|
| win | 385 | 0.4771 | 0.3351 | +0.1421 | 🟡+30% | 0.2350 |

### 戦略別: 校正精度 + Brier Skill Score
| sid | bt | n | pred | actual | Brier | BSS | ROI |
|---|---|---|---|---|---|---|---|
| S00 | win | 157 | 0.4371 | 0.2866 | 0.2217 | 🔴-0.08 | 0.779 |
| S01_NAKAANA1 | win | 163 | 0.4865 | 0.3313 | 0.2372 | 🔴-0.07 | 0.771 |
| S02_TETSUBAN | win | 65 | 0.5502 | 0.4615 | 0.2619 | 🔴-0.05 | 1.049 |

### 確率デシル別: 校正カーブ
| 確率帯 | n | 予測avg | 実的中率 | gap |
|---|---|---|---|---|
| 0.15-0.20 | 8 | 0.1878 | 0.0000 | 🔴+0.1878 |
| 0.20-0.30 | 9 | 0.2290 | 0.1111 | 🔴+0.1179 |
| 0.30-0.50 | 139 | 0.4139 | 0.3022 | 🔴+0.1117 |
| 0.50+ | 224 | 0.5450 | 0.3795 | 🔴+0.1655 |

## Settlement Ratio データ品質

- 学習済み: 4バンド / fallback: 13バンド
| bt | odds帯 | source | n | ratio |
|---|---|---|---|---|
| win | <3.0 | ✅learned | 198 | 0.809 |
| win | <5.0 | ✅learned | 365 | 0.74 |
| win | <10.0 | ✅learned | 157 | 0.451 |
| win | <20.0 | ✅learned | 47 | 0.249 |
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
_auto-generated by claude_snapshot.py at 2026-11-05T12:40:01.287282+09:00_