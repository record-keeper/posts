# ClaudeDebug スナップショット

## 🔴 現状: RED

**生成**: 2026-10-24T11:30:01.809840+09:00

### 次に取るべきアクション
> RED最優先: CIRCUIT_BREAKER_TRIP×53 (24h) → ログ/DB確認

### 検出された問題
- 🟡 FINAL_MISSING×87 (24h)
- 🔴 CIRCUIT_BREAKER_TRIP×53 (24h)
- 🔴 STRATEGY_CI_FAIL×17 (24h)
- 🟡 LARGE_ODDS_DRIFT×3 (24h)
- 🔴 SEND_WITHOUT_DBREC×1 (24h)
- 🔴 alert_manager dispatch 失敗確定 1件（手動確認必要）

---

## 🔧 AI デバッグキュー（このClaudeが対処）

### 🔴 CIRCUIT_BREAKER_TRIP  ×54  [2026-10-24T11:01:46]
- key: `CIRCUIT_BREAKER_TRIP|`
- **FIX**: 7日ROI<0.7→戦略を enabled:false にして原因調査。校正ドリフトか市場変化を確認

### 🔴 CIRCUIT_BREAKER_NO_ACTION  ×54  [2026-10-24T11:01:46]
- key: `CIRCUIT_BREAKER_NO_ACTION|`
- **FIX**: CIRCUIT_BREAKER_TRIP 発動済なのに strategies.json で enabled のまま。enabled:false に切替 or 復旧条件満たしたか確認

### 🔴 STRATEGY_CI_FAIL  ×27  [2026-10-24T11:01:46]
- key: `STRATEGY_CI_FAIL|`
- **FIX**: grid戦略のOOS CI下限<1.0→論文基準で赤字リスク。strategies.json確認

### 🔴 CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION  ×2  [2026-10-24T11:00:03]
- key: `CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION|戦略 S00 が TRIP してるが enabled のまま`
- **FIX**: CIRCUIT_BREAKER_TRIP 戦略が enabled のまま。enabled:false に

### 🔴 CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION  ×2  [2026-10-24T11:00:03]
- key: `CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION|戦略 S01_NAKAANA1 が TRIP してるが enabled のまま`
- **FIX**: CIRCUIT_BREAKER_TRIP 戦略が enabled のまま。enabled:false に

### 🟡 ANOMALY_SCAN_FINAL_RATIO  ×21  [2026-10-24T10:52:28]
- key: `ANOMALY_SCAN_FINAL_RATIO|`
- **FIX**: scan→final成立率が7日baselineから2σ逸脱。scan/final window設定・odds取得タイミング

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-10-24T06:00:17]
- key: `INSUFFICIENT_SAMPLE|S02_TETSUBAN: n=79<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-10-24T06:00:17]
- key: `INSUFFICIENT_SAMPLE|S01_NAKAANA1: n=189<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-10-24T06:00:17]
- key: `INSUFFICIENT_SAMPLE|S00: n=180<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ CALIBRATION_LIVE  ×1  [2026-10-24T06:00:17]
- key: `CALIBRATION_LIVE|decile 0.10-0.15: n=6 pred=0.1269 actual=0.3333 gap=-0.2064`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ DRIFT_BUCKET  ×1  [2026-10-24T06:00:17]
- key: `DRIFT_BUCKET|drift +10%〜+30%: n=66 hit%=31.8% ROI=0.83 (コスト 15,700/回収 13,040)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ CALIBRATION_LIVE  ×1  [2026-10-24T06:00:17]
- key: `CALIBRATION_LIVE|decile 0.15-0.20: n=8 pred=0.1824 actual=0.0000 gap=+0.1824`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-10-24T06:00:17]
- key: `CALIBRATION_LIVE|decile 0.20-0.30: n=8 pred=0.2288 actual=0.2500 gap=-0.0212`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-10-24T06:00:17]
- key: `ROI_STAT|S00: n=180 hit%=28.9% hit_CI[Bonf]=[20.2,39.4]% ROI=0.79 ROI_boot95=[0.58,1.02]`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-10-24T06:00:17]
- key: `ROI_STAT|S01_NAKAANA1: n=189 hit%=33.3% hit_CI[Bonf]=[24.3,43.8]% ROI=0.91 ROI_boot95=[0.`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-10-24T06:00:17]
- key: `ROI_STAT|S02_TETSUBAN: n=79 hit%=51.9% hit_CI[Bonf]=[36.3,67.2]% ROI=0.95 ROI_boot95=[0.7`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### 🟡 ORPHAN_SCAN  ×1  [2026-10-24T06:00:17]
- key: `ORPHAN_SCAN|159 件の scan に final/retreat 追従無し`
- **FIX**: scan 後 final も retreat も無い→当該レースの final 窓が短すぎ/fetch 失敗

### ℹ️ DRIFT_BUCKET  ×1  [2026-10-24T06:00:17]
- key: `DRIFT_BUCKET|drift ≤-30%: n=27 hit%=48.1% ROI=1.23 (コスト 7,800/回収 9,630)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-10-24T06:00:17]
- key: `DRIFT_BUCKET|drift -30%〜-10%: n=46 hit%=34.8% ROI=0.74 (コスト 10,900/回収 8,120)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-10-24T06:00:17]
- key: `DRIFT_BUCKET|drift -10%〜+10%: n=90 hit%=40.0% ROI=1.12 (コスト 20,400/回収 22,860)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料


以下、詳細セクション（通常読み飛ばし可）

## 環境・コード状態
- git_sha: `<error: Command '['git', '-C', '/opt/boa` dirty=True
- config.json md5: `eb532e851a30cd2f7e69bdf0dfca3f2b`
- strategies.json md5: `06b22dd935785e7947bf9c0f170b69a3`
- numpy=2.4.4 lightgbm=4.6.0 scipy=1.17.1
- **calibration_applied**: True ← predictor.py が校正を呼んでるか
- DB: 16.62MB / last modified 2026-10-24T11:30:05.728317+09:00

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
00, 'A': 6000, 'B': 1500} default=5000
2026-10-24 11:28:04,663 [INFO] predictor: Models loaded OK
2026-10-24 11:28:15,841 [WARNING] scraper: fetch error (1/3): https://www.boatrace.jp/owpc/pc/race/racelist?rno=7&jcd=21&hd=20261024: HTTPSConnectionPool(host='www.boatrace.jp', port=443): Read timed out. (read timeout=10), retry in 1s
2026-10-24 11:28:26,922 [WARNING] scraper: fetch error (2/3): https://www.boatrace.jp/owpc/pc/race/racelist?rno=7&jcd=21&hd=20261024: HTTPSConnectionPool(host='www.boatrace.jp', port=443): Read timed out. (read timeout=10), retry in 3s
2026-10-24 11:28:39,969 [WARNING] scraper: fetch error (3/3): https://www.boatrace.jp/owpc/pc/race/racelist?rno=7&jcd=21&hd=20261024: HTTPSConnectionPool(host='www.boatrace.jp', port=443): Read timed out. (read timeout=10), retry in 9s
2026-10-24 11:28:39,970 [ERROR] scraper: fetch failed after 3 retries: https://www.boatrace.jp/owpc/pc/race/racelist?rno=7&jcd=21&hd=20261024
2026-10-24 11:28:39,970 [ERROR] scraper: racelist fetch failed: jcd=21 rno=7
2026-10-24 11:28:39,970 [WARNING] run_cycle: fetch None: 21/7
2026-10-24 11:28:51,002 [WARNING] scraper: fetch error (1/3): https://www.boatrace.jp/owpc/pc/race/racelist?rno=7&jcd=10&hd=20261024: HTTPSConnectionPool(host='www.boatrace.jp', port=443): Read timed out. (read timeout=10), retry in 1s
2026-10-24 11:29:02,420 [INFO] scraper: odds3t: 120/120 parsed
2026-10-24 11:29:03,538 [INFO] scraper: odds3f: 20/20 parsed
2026-10-24 11:29:04,654 [INFO] scraper: odds2t: 30/30 parsed
2026-10-24 11:29:04,655 [INFO] scraper: odds2f: 15/15 parsed
2026-10-24 11:29:05,750 [INFO] scraper: odds_win: 5/6 parsed
2026-10-24 11:29:05,750 [INFO] scraper: fetch_race 10/7: boats=6 odds=190/191
2026-10-24 11:29:05,754 [INFO] predictor: CALIBRATION_MODE=on
2026-10-24 11:29:05,754 [INFO] predictor: combos: {'win': 5, '2t': 30, '3t': 120}
2026-10-24 11:29:05,758 [INFO] run_cycle: fetched 10/7 [scan]: 155 combos
2026-10-24 11:29:06,023 [INFO] run_cycle: run_cycle done: 0 notifications

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
    "c": 73
  },
  {
    "target": "primary",
    "ok": 1,
    "c": 73
  }
]
```

## Phase別通知記録 (24h)
{'final': 29, 'result': 18, 'scan': 26}

## アラート件数 (24h・種類別)
```
  ANOMALY_SCRAPER_FAILURE_BURST: 141
  FINAL_MISSING: 87
  CIRCUIT_BREAKER_TRIP: 53
  CIRCUIT_BREAKER_NO_ACTION: 34
  ANOMALY_SCAN_FINAL_RATIO: 32
  STRATEGY_CI_FAIL: 17
  LARGE_ODDS_DRIFT: 3
  SEND_WITHOUT_DBREC: 1
```

## 戦略別 ROI (7日)
| sid | n | hits | cost | payout | PL | ROI |
|---|---|---|---|---|---|---|
| S00 | 35 | 8 | 10,500 | 6,420 | -4,080 | 0.611 |
| S01_NAKAANA1 | 53 | 11 | 10,600 | 4,700 | -5,900 | 0.443 |
| S02_TETSUBAN | 14 | 7 | 2,800 | 3,140 | +340 | 1.121 |

## 直近アラート (24h・新しい順)
```
[11:29:06] CIRCUIT_BREAKER_TRIP: {"cost": 10500, "kind": "CIRCUIT_BREAKER_TRIP", "n": 35, "payout": 6420, "roi_7d": 0.611, "sid": "S00"}
[11:20:22] CIRCUIT_BREAKER_TRIP: {"cost": 10800, "kind": "CIRCUIT_BREAKER_TRIP", "n": 36, "payout": 6420, "roi_7d": 0.594, "sid": "S00"}
[11:14:39] CIRCUIT_BREAKER_TRIP: {"cost": 10600, "kind": "CIRCUIT_BREAKER_TRIP", "n": 53, "payout": 4700, "roi_7d": 0.443, "sid": "S01_NAKAANA1"}
[11:14:39] LARGE_ODDS_DRIFT: {"combo": "1", "drift_pct": 53.3, "final": 4.6, "kind": "LARGE_ODDS_DRIFT", "race": "113R", "scan": 3.0, "sid": "S01_NAKAANA1"}
[11:14:39] ANOMALY_SCAN_FINAL_RATIO: {"abs_drop": -0.178, "baseline_mean": 0.822, "baseline_stdev": 0.075, "kind": "ANOMALY_SCAN_FINAL_RATIO", "today_ratio": 1.0, "today_scan_count": 5, "z_score": 2.37}
[11:06:28] CIRCUIT_BREAKER_TRIP: {"cost": 10800, "kind": "CIRCUIT_BREAKER_TRIP", "n": 36, "payout": 5790, "roi_7d": 0.536, "sid": "S00"}
[11:06:28] ANOMALY_SCAN_FINAL_RATIO: {"abs_drop": -0.178, "baseline_mean": 0.822, "baseline_stdev": 0.075, "kind": "ANOMALY_SCAN_FINAL_RATIO", "today_ratio": 1.0, "today_scan_count": 4, "z_score": 2.37}
[11:01:43] STRATEGY_CI_FAIL: {"ci_lo": null, "kind": "STRATEGY_CI_FAIL", "sid": "S02_TETSUBAN"}
[11:01:43] CIRCUIT_BREAKER_NO_ACTION: {"kind": "CIRCUIT_BREAKER_NO_ACTION", "sid": "S01_NAKAANA1"}
[11:01:43] CIRCUIT_BREAKER_NO_ACTION: {"kind": "CIRCUIT_BREAKER_NO_ACTION", "sid": "S00"}
```

## 本日残レース: 130件

## 本日nidレジャー（ID単位完遂突合せ）
- race_schedule: 168件 登録 / 38件 締切済
- 通知発射: scan=6 nid / final=6 nid / result=2 nid
- predictions: 5 / うち結果DB記録済: 3
- ✅ 結果DBあるが通知未発射: 0件 `tools/backfill_result_notifications.py` で救済可
- ✅ scan後final無しのまま締切: 0件（FINAL_MISSING の温床）

## 直近送信失敗 (24h)
```
```

## 最新 predictions サンプル (計算spot-check用)
| sid | race | bt | combo | p | odds | ev | bet | at |
|---|---|---|---|---|---|---|---|---|
| S01_NAKAANA1 | 113R | win | 1 | 0.3177 | 4.6 | 1.46 | 200 | scan=3.0 drift=+53.3% | 11:14:30 |
| S00 | 132R | win | 1 | 0.1957 | 4.2 | 0.82 | 300 | scan=6.3 drift=-33.3% | 11:06:20 |
| S00 | 041R | win | 1 | 0.5891 | 7.1 | 4.18 | 300 | scan=8.7 drift=-18.4% | 10:49:19 |
| S01_NAKAANA1 | 142R | win | 1 | 0.5123 | 4.5 | 2.31 | 200 | scan=- drift=- | 08:58:31 |
| S00 | 142R | win | 1 | 0.5123 | 4.5 | 2.31 | 300 | scan=- drift=- | 08:58:29 |
| S01_NAKAANA1 | 204R | win | 1 | 0.5123 | 3.8 | 1.95 | 200 | scan=- drift=- | 19:28:19 |
| S01_NAKAANA1 | 249R | win | 1 | 0.4111 | 3.6 | 1.48 | 200 | scan=3.6 drift=+0.0% | 19:14:29 |
| S00 | 202R | win | 1 | 0.3177 | 4.9 | 1.56 | 300 | scan=4.3 drift=+14.0% | 18:31:18 |
| S01_NAKAANA1 | 0610R | win | 1 | 0.5891 | 4.0 | 2.36 | 200 | scan=- drift=- | 15:09:18 |
| S00 | 1710R | win | 1 | 0.3177 | 4.5 | 1.43 | 300 | scan=- drift=- | 14:29:19 |

## オッズドリフト統計 (7日)

| bt | n | avg | min | max | down10 | collapse(≤-30%) | any_large(≥10%) |
|---|---|---|---|---|---|---|---|
| win | 60 | +28.1% | -52.3% | +495.8% | 9 | 2 | 37 |

## 校正テーブル合格状況

- total: 27 グループ
- passed: 19
- failed: 8 — `2f|4, 2f|5, 3f|2, 3f|3, 3f|4, 3t|1, 3t|4, 3t|5`
- 主力グループ状態: ✅ (全12グループ合格)

## SRE Golden Signals (24h)

| Signal | Value |
|---|---|
| **Latency** (scan→final avg) | 443.1s |
| **Latency** (scan→final max) | 600.3s |
| **Traffic** (notifications 24h) | 73 |
| **Errors** (send fail rate) | ✅ 0.0% |
| **Saturation** (S00) | 900円 used |
| **Saturation** (S01_NAKAANA1) | 400円 used |

## 信ぴょう性メトリクス（予測精度の証拠）

### bt別: 予測確率 vs 実的中率
| bt | n | 予測avg | 実的中率 | 校正誤差 | 過信度 | Brier |
|---|---|---|---|---|---|---|
| win | 448 | 0.4801 | 0.3460 | +0.1341 | 🟡+28% | 0.2428 |

### 戦略別: 校正精度 + Brier Skill Score
| sid | bt | n | pred | actual | Brier | BSS | ROI |
|---|---|---|---|---|---|---|---|
| S00 | win | 180 | 0.4396 | 0.2889 | 0.2361 | 🔴-0.15 | 0.791 |
| S01_NAKAANA1 | win | 190 | 0.4923 | 0.3316 | 0.2429 | 🔴-0.10 | 0.905 |
| S02_TETSUBAN | win | 78 | 0.5436 | 0.5128 | 0.2581 | 🔴-0.03 | 0.942 |

### 確率デシル別: 校正カーブ
| 確率帯 | n | 予測avg | 実的中率 | gap |
|---|---|---|---|---|
| 0.10-0.15 | 6 | 0.1269 | 0.3333 | 🔴-0.2064 |
| 0.15-0.20 | 7 | 0.1839 | 0.0000 | 🔴+0.1839 |
| 0.20-0.30 | 8 | 0.2288 | 0.2500 | ✅-0.0212 |
| 0.30-0.50 | 156 | 0.4134 | 0.3077 | 🔴+0.1057 |
| 0.50+ | 270 | 0.5430 | 0.3778 | 🔴+0.1653 |

## Settlement Ratio データ品質

- 学習済み: 4バンド / fallback: 13バンド
| bt | odds帯 | source | n | ratio |
|---|---|---|---|---|
| win | <3.0 | ✅learned | 192 | 0.781 |
| win | <5.0 | ✅learned | 344 | 0.746 |
| win | <10.0 | ✅learned | 151 | 0.456 |
| win | <20.0 | ✅learned | 43 | 0.254 |
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
_auto-generated by claude_snapshot.py at 2026-10-24T11:30:01.809840+09:00_