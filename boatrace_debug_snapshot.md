# ClaudeDebug スナップショット

## 🔴 現状: RED

**生成**: 2026-11-24T16:10:01.821143+09:00

### 次に取るべきアクション
> RED最優先: CRITICAL_ODDS_COLLAPSE×1 (24h) → ログ/DB確認

### 検出された問題
- 🟡 FINAL_MISSING×163 (24h)
- 🔴 PSI_DRIFT_DETECTED×29 (24h)
- 🔴 STRATEGY_CI_FAIL×17 (24h)
- 🔴 CRITICAL_ODDS_COLLAPSE×1 (24h)
- 🔴 alert_manager dispatch 失敗確定 1件（手動確認必要）

---

## 🔧 AI デバッグキュー（このClaudeが対処）

### 🟡 CODE_AUDIT_SCRAPER_FAILURE_RATE_HIGH  ×1  [2026-11-24T16:00:03]
- key: `CODE_AUDIT_SCRAPER_FAILURE_RATE_HIGH|直近 500 log行 で 3-retry 全敗 13 件 (閾値 3)`
- **FIX**: scraper 3-retry 全敗多発。boatrace.jp timeout or IP ban 疑い

### 🟡 ANOMALY_SCRAPER_FAILURE_BURST  ×5  [2026-11-24T15:36:15]
- key: `ANOMALY_SCRAPER_FAILURE_BURST|`
- **FIX**: 直近1h でscraper 3-retry 全敗多発。boatrace.jp 側timeout / IP ban / DDoS

### 🟡 CODE_AUDIT_SCRAPER_FAILURE_RATE_HIGH  ×1  [2026-11-24T15:30:02]
- key: `CODE_AUDIT_SCRAPER_FAILURE_RATE_HIGH|直近 500 log行 で 3-retry 全敗 4 件 (閾値 3)`
- **FIX**: scraper 3-retry 全敗多発。boatrace.jp timeout or IP ban 疑い

### 🔴 PSI_DRIFT_DETECTED  ×7  [2026-11-24T15:22:41]
- key: `PSI_DRIFT_DETECTED|`
- **FIX**: ml_prob 分布の PSI>0.25→モデル入力の分布シフト。校正テーブル再生成 or モデル再学習を検討

### 🔴 STRATEGY_CI_FAIL  ×7  [2026-11-24T15:22:41]
- key: `STRATEGY_CI_FAIL|`
- **FIX**: grid戦略のOOS CI下限<1.0→論文基準で赤字リスク。strategies.json確認

### 🟡 CODE_AUDIT_SCRAPER_FAILURE_RATE_HIGH  ×1  [2026-11-24T15:00:04]
- key: `CODE_AUDIT_SCRAPER_FAILURE_RATE_HIGH|直近 500 log行 で 3-retry 全敗 5 件 (閾値 3)`
- **FIX**: scraper 3-retry 全敗多発。boatrace.jp timeout or IP ban 疑い

### 🟡 CODE_AUDIT_SCRAPER_FAILURE_RATE_HIGH  ×1  [2026-11-24T14:30:04]
- key: `CODE_AUDIT_SCRAPER_FAILURE_RATE_HIGH|直近 500 log行 で 3-retry 全敗 8 件 (閾値 3)`
- **FIX**: scraper 3-retry 全敗多発。boatrace.jp timeout or IP ban 疑い

### 🟡 CODE_AUDIT_SCRAPER_FAILURE_RATE_HIGH  ×1  [2026-11-24T14:00:03]
- key: `CODE_AUDIT_SCRAPER_FAILURE_RATE_HIGH|直近 500 log行 で 3-retry 全敗 9 件 (閾値 3)`
- **FIX**: scraper 3-retry 全敗多発。boatrace.jp timeout or IP ban 疑い

### 🟡 ANOMALY_SCAN_FINAL_RATIO  ×3  [2026-11-24T13:14:39]
- key: `ANOMALY_SCAN_FINAL_RATIO|`
- **FIX**: scan→final成立率が7日baselineから2σ逸脱。scan/final window設定・odds取得タイミング

### 🟡 CODE_AUDIT_SCRAPER_FAILURE_RATE_HIGH  ×2  [2026-11-24T12:00:03]
- key: `CODE_AUDIT_SCRAPER_FAILURE_RATE_HIGH|直近 500 log行 で 3-retry 全敗 7 件 (閾値 3)`
- **FIX**: scraper 3-retry 全敗多発。boatrace.jp timeout or IP ban 疑い

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-11-24T06:00:19]
- key: `INSUFFICIENT_SAMPLE|S00: n=71<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-11-24T06:00:19]
- key: `INSUFFICIENT_SAMPLE|S02_TETSUBAN: n=40<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-11-24T06:00:19]
- key: `INSUFFICIENT_SAMPLE|S01_NAKAANA1: n=90<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ ROI_STAT  ×1  [2026-11-24T06:00:19]
- key: `ROI_STAT|S00: n=71 hit%=22.5% hit_CI[Bonf]=[11.6,39.3]% ROI=0.57 ROI_boot95=[0.31,0.88]`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-11-24T06:00:19]
- key: `ROI_STAT|S01_NAKAANA1: n=90 hit%=33.3% hit_CI[Bonf]=[20.9,48.5]% ROI=0.85 ROI_boot95=[0.5`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-11-24T06:00:19]
- key: `ROI_STAT|S02_TETSUBAN: n=40 hit%=40.0% hit_CI[Bonf]=[21.3,62.1]% ROI=1.15 ROI_boot95=[0.5`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### 🟡 ORPHAN_SCAN  ×1  [2026-11-24T06:00:19]
- key: `ORPHAN_SCAN|266 件の scan に final/retreat 追従無し`
- **FIX**: scan 後 final も retreat も無い→当該レースの final 窓が短すぎ/fetch 失敗

### ℹ️ DRIFT_BUCKET  ×1  [2026-11-24T06:00:19]
- key: `DRIFT_BUCKET|drift -30%〜-10%: n=23 hit%=17.4% ROI=0.77 (コスト 5,000/回収 3,860)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-11-24T06:00:19]
- key: `DRIFT_BUCKET|drift -10%〜+10%: n=38 hit%=44.7% ROI=1.14 (コスト 8,700/回収 9,890)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ CALIBRATION_LIVE  ×1  [2026-11-24T06:00:19]
- key: `CALIBRATION_LIVE|bt=win: n=201 pred=0.4776 actual=0.3085 error=+0.1692 (+35%) brier=0.2354 [OVERC`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用


以下、詳細セクション（通常読み飛ばし可）

## 環境・コード状態
- git_sha: `<error: Command '['git', '-C', '/opt/boa` dirty=True
- config.json md5: `eb532e851a30cd2f7e69bdf0dfca3f2b`
- strategies.json md5: `06b22dd935785e7947bf9c0f170b69a3`
- numpy=2.4.4 lightgbm=4.6.0 scipy=1.17.1
- **calibration_applied**: True ← predictor.py が校正を呼んでるか
- DB: 18.62MB / last modified 2026-11-24T16:07:59.277945+09:00

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
race/oddstf?rno=3&jcd=07&hd=20261124: HTTPSConnectionPool(host='www.boatrace.jp', port=443): Read timed out. (read timeout=10), retry in 1s
2026-11-24 16:07:58,124 [INFO] scraper: odds_win: 5/6 parsed
2026-11-24 16:07:58,124 [INFO] scraper: fetch_race 07/3: boats=6 odds=190/191
2026-11-24 16:07:58,128 [INFO] predictor: CALIBRATION_MODE=on
2026-11-24 16:07:58,128 [INFO] predictor: combos: {'win': 5, '2t': 30, '3t': 120}
2026-11-24 16:07:58,133 [INFO] run_cycle: fetched 07/3 [final]: 155 combos
2026-11-24 16:07:58,428 [INFO] race_id: notif: nid=2026112407031608 sid=S00 phase=final rank=SSS
2026-11-24 16:07:58,759 [INFO] notifier: Discord notify OK (status=204)
2026-11-24 16:07:59,252 [INFO] notifier: Discord notify OK (status=204)
2026-11-24 16:07:59,278 [INFO] run_cycle: FINAL S00 蒲郡3R SSS
2026-11-24 16:08:28,840 [INFO] scraper: odds3t: 120/120 parsed
2026-11-24 16:08:37,949 [INFO] scraper: odds3f: 20/20 parsed
2026-11-24 16:08:48,961 [WARNING] scraper: fetch error (1/3): https://www.boatrace.jp/owpc/pc/race/odds2tf?rno=3&jcd=19&hd=20261124: HTTPSConnectionPool(host='www.boatrace.jp', port=443): Read timed out. (read timeout=10), retry in 1s
2026-11-24 16:08:58,108 [INFO] scraper: odds2t: 29/30 parsed
2026-11-24 16:08:58,109 [INFO] scraper: odds2f: 14/15 parsed
2026-11-24 16:09:07,242 [INFO] scraper: odds_win: 2/6 parsed
2026-11-24 16:09:07,242 [INFO] scraper: fetch_race 19/3: boats=6 odds=185/191
2026-11-24 16:09:07,245 [INFO] predictor: CALIBRATION_MODE=on
2026-11-24 16:09:07,245 [INFO] predictor: combos: {'win': 2, '2t': 29, '3t': 120}
2026-11-24 16:09:07,249 [INFO] run_cycle: fetched 19/3 [scan]: 151 combos
2026-11-24 16:09:27,570 [WARNING] scraper: fetch error (1/3): https://www.boatrace.jp/owpc/pc/race/beforeinfo?rno=3&jcd=24&hd=20261124: HTTPSConnectionPool(host='www.boatrace.jp', port=443): Read timed out. (read timeout=10), retry in 1s
2026-11-24 16:09:45,880 [INFO] scraper: odds3t: 120/120 parsed
2026-11-24 16:09:54,973 [INFO] scraper: odds3f: 20/20 parsed

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
    "c": 41
  },
  {
    "target": "primary",
    "ok": 1,
    "c": 41
  }
]
```

## Phase別通知記録 (24h)
{'final': 13, 'result': 5, 'scan': 23}

## アラート件数 (24h・種類別)
```
  ANOMALY_SCRAPER_FAILURE_BURST: 225
  FINAL_MISSING: 163
  PSI_DRIFT_DETECTED: 29
  STRATEGY_CI_FAIL: 17
  ANOMALY_SCAN_FINAL_RATIO: 2
  ANOMALY_BET_VOLUME_SPIKE: 1
  CRITICAL_ODDS_COLLAPSE: 1
```

## 戦略別 ROI (7日)
| sid | n | hits | cost | payout | PL | ROI |
|---|---|---|---|---|---|---|
| S00 | 9 | 2 | 2,700 | 1,380 | -1,320 | 0.511 |
| S01_NAKAANA1 | 19 | 7 | 3,800 | 2,880 | -920 | 0.758 |
| S02_TETSUBAN | 4 | 2 | 800 | 2,160 | +1,360 | 2.7 |

## 直近アラート (24h・新しい順)
```
[16:05:23] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 13, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 507}
[15:59:57] FINAL_MISSING: {"deadline": "2026-11-24T15:29:00+09:00", "kind": "FINAL_MISSING", "nid": "2026112422101529", "sid": "S01_NAKAANA1"}
[15:59:57] FINAL_MISSING: {"deadline": "2026-11-24T13:19:00+09:00", "kind": "FINAL_MISSING", "nid": "2026112405071319", "sid": "S02_TETSUBAN"}
[15:59:57] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 13, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 497}
[15:51:39] PSI_DRIFT_DETECTED: {"bt": "win", "kind": "PSI_DRIFT_DETECTED", "n_baseline": 163, "n_recent": 31, "psi": 0.549}
[15:51:39] FINAL_MISSING: {"deadline": "2026-11-24T11:04:00+09:00", "kind": "FINAL_MISSING", "nid": "2026112421061104", "sid": "S02_TETSUBAN"}
[15:51:39] FINAL_MISSING: {"deadline": "2026-11-24T15:19:00+09:00", "kind": "FINAL_MISSING", "nid": "2026112407011519", "sid": "S00"}
[15:51:39] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 9, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 494}
[15:43:07] FINAL_MISSING: {"deadline": "2026-11-24T14:05:00+09:00", "kind": "FINAL_MISSING", "nid": "2026112413081405", "sid": "S00"}
[15:43:07] FINAL_MISSING: {"deadline": "2026-11-24T11:02:00+09:00", "kind": "FINAL_MISSING", "nid": "2026112409021102", "sid": "S01_NAKAANA1"}
```

## 本日残レース: 50件

## 本日nidレジャー（ID単位完遂突合せ）
- race_schedule: 180件 登録 / 130件 締切済
- 通知発射: scan=19 nid / final=9 nid / result=2 nid
- predictions: 4 / うち結果DB記録済: 3
- ✅ 結果DBあるが通知未発射: 0件 `tools/backfill_result_notifications.py` で救済可
- 🔴 scan後final無しのまま締切: 11件（FINAL_MISSING の温床）

## 直近送信失敗 (24h)
```
```

## 最新 predictions サンプル (計算spot-check用)
| sid | race | bt | combo | p | odds | ev | bet | at |
|---|---|---|---|---|---|---|---|---|
| S00 | 073R | win | 1 | 0.4989 | 10.1 | 5.04 | 300 | scan=7.5 drift=+34.7% | 16:07:58 |
| S01_NAKAANA1 | 098R | win | 1 | 0.4111 | 4.6 | 1.89 | 200 | scan=- drift=- | 13:59:52 |
| S00 | 098R | win | 1 | 0.4111 | 4.6 | 1.89 | 300 | scan=11.2 drift=-58.9% | 13:59:50 |
| S02_TETSUBAN | 212R | win | 1 | 0.5334 | 2.8 | 1.49 | 200 | scan=- drift=- | 09:08:14 |
| S01_NAKAANA1 | 074R | win | 1 | 0.5719 | 3.5 | 2.00 | 200 | scan=3.1 drift=+12.9% | 16:34:46 |
| S01_NAKAANA1 | 122R | win | 1 | 0.5123 | 3.3 | 1.69 | 200 | scan=- drift=- | 15:49:13 |
| S01_NAKAANA1 | 135R | win | 1 | 0.5123 | 4.1 | 2.10 | 200 | scan=- drift=- | 12:38:14 |
| S01_NAKAANA1 | 023R | win | 1 | 0.5104 | 3.5 | 1.79 | 200 | scan=3.0 drift=+16.7% | 11:38:24 |
| S00 | 107R | win | 1 | 0.5123 | 24.0 | 12.30 | 300 | scan=- drift=- | 11:34:39 |
| S02_TETSUBAN | 052R | win | 1 | 0.5080 | 2.1 | 1.07 | 200 | scan=- drift=- | 11:00:54 |

## オッズドリフト統計 (7日)

| bt | n | avg | min | max | down10 | collapse(≤-30%) | any_large(≥10%) |
|---|---|---|---|---|---|---|---|
| win | 15 | +1.0% | -58.9% | +34.7% | 4 | 1 | 9 |

## 校正テーブル合格状況

- total: 27 グループ
- passed: 19
- failed: 8 — `2f|4, 2f|5, 3f|2, 3f|3, 3f|4, 3t|1, 3t|4, 3t|5`
- 主力グループ状態: ✅ (全12グループ合格)

## SRE Golden Signals (24h)

| Signal | Value |
|---|---|
| **Latency** (scan→final avg) | 387.1s |
| **Latency** (scan→final max) | 611.9s |
| **Traffic** (notifications 24h) | 41 |
| **Errors** (send fail rate) | ✅ 0.0% |
| **Saturation** (S00) | 600円 used |
| **Saturation** (S01_NAKAANA1) | 200円 used |
| **Saturation** (S02_TETSUBAN) | 200円 used |

## 信ぴょう性メトリクス（予測精度の証拠）

### bt別: 予測確率 vs 実的中率
| bt | n | 予測avg | 実的中率 | 校正誤差 | 過信度 | Brier |
|---|---|---|---|---|---|---|
| win | 194 | 0.4748 | 0.2990 | +0.1758 | 🟡+37% | 0.2350 |

### 戦略別: 校正精度 + Brier Skill Score
| sid | bt | n | pred | actual | Brier | BSS | ROI |
|---|---|---|---|---|---|---|---|
| S00 | win | 66 | 0.4210 | 0.2121 | 0.2064 | 🔴-0.24 | 0.574 |
| S01_NAKAANA1 | win | 87 | 0.4805 | 0.3103 | 0.2416 | 🔴-0.13 | 0.825 |
| S02_TETSUBAN | win | 41 | 0.5492 | 0.4146 | 0.2673 | 🔴-0.10 | 1.18 |

### 確率デシル別: 校正カーブ
| 確率帯 | n | 予測avg | 実的中率 | gap |
|---|---|---|---|---|
| 0.30-0.50 | 78 | 0.4122 | 0.2821 | 🔴+0.1301 |
| 0.50+ | 108 | 0.5437 | 0.3333 | 🔴+0.2104 |

## Settlement Ratio データ品質

- 学習済み: 4バンド / fallback: 13バンド
| bt | odds帯 | source | n | ratio |
|---|---|---|---|---|
| win | <3.0 | ✅learned | 209 | 0.818 |
| win | <5.0 | ✅learned | 381 | 0.737 |
| win | <10.0 | ✅learned | 160 | 0.449 |
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
_auto-generated by claude_snapshot.py at 2026-11-24T16:10:01.821143+09:00_