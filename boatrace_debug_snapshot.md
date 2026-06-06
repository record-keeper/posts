# ClaudeDebug スナップショット

## 🔴 現状: RED

**生成**: 2026-06-06T12:30:02.236379+09:00

### 次に取るべきアクション
> RED最優先: CIRCUIT_BREAKER_TRIP×63 (24h) → ログ/DB確認

### 検出された問題
- 🔴 CIRCUIT_BREAKER_TRIP×63 (24h)
- 🟡 FINAL_MISSING×27 (24h)
- 🔴 STRATEGY_CI_FAIL×17 (24h)
- 🟡 LARGE_ODDS_DRIFT×2 (24h)
- 🔴 alert_manager dispatch 失敗確定 1件（手動確認必要）

---

## 🔧 AI デバッグキュー（このClaudeが対処）

### 🔴 CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION  ×1  [2026-06-06T12:30:04]
- key: `CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION|戦略 S00 が TRIP してるが enabled のまま`
- **FIX**: CIRCUIT_BREAKER_TRIP 戦略が enabled のまま。enabled:false に

### 🔴 CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION  ×1  [2026-06-06T12:30:04]
- key: `CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION|戦略 S01_NAKAANA1 が TRIP してるが enabled のまま`
- **FIX**: CIRCUIT_BREAKER_TRIP 戦略が enabled のまま。enabled:false に

### 🔴 CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION  ×1  [2026-06-06T12:30:04]
- key: `CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION|戦略 S02_TETSUBAN が TRIP してるが enabled のまま`
- **FIX**: CIRCUIT_BREAKER_TRIP 戦略が enabled のまま。enabled:false に

### 🔴 CIRCUIT_BREAKER_TRIP  ×84  [2026-06-06T12:02:30]
- key: `CIRCUIT_BREAKER_TRIP|`
- **FIX**: 7日ROI<0.7→戦略を enabled:false にして原因調査。校正ドリフトか市場変化を確認

### 🔴 CIRCUIT_BREAKER_NO_ACTION  ×84  [2026-06-06T12:02:30]
- key: `CIRCUIT_BREAKER_NO_ACTION|`
- **FIX**: CIRCUIT_BREAKER_TRIP 発動済なのに strategies.json で enabled のまま。enabled:false に切替 or 復旧条件満たしたか確認

### 🔴 STRATEGY_CI_FAIL  ×28  [2026-06-06T12:02:30]
- key: `STRATEGY_CI_FAIL|`
- **FIX**: grid戦略のOOS CI下限<1.0→論文基準で赤字リスク。strategies.json確認

### 🟡 ANOMALY_SCAN_FINAL_RATIO  ×28  [2026-06-06T11:44:35]
- key: `ANOMALY_SCAN_FINAL_RATIO|`
- **FIX**: scan→final成立率が7日baselineから2σ逸脱。scan/final window設定・odds取得タイミング

### 🟡 ANOMALY_SCRAPER_FAILURE_BURST  ×6  [2026-06-06T10:17:42]
- key: `ANOMALY_SCRAPER_FAILURE_BURST|`
- **FIX**: 直近1h でscraper 3-retry 全敗多発。boatrace.jp 側timeout / IP ban / DDoS

### 🟡 ANOMALY_BET_VOLUME_DROP  ×60  [2026-06-06T09:00:26]
- key: `ANOMALY_BET_VOLUME_DROP|`
- **FIX**: 本日のbet数が7日baselineから2σ低下。戦略filter/ scan fix/run_cycle停止を疑え

### ℹ️ CALIBRATION_LIVE  ×1  [2026-06-06T06:00:12]
- key: `CALIBRATION_LIVE|decile 0.15-0.20: n=6 pred=0.1957 actual=0.1667 gap=+0.0291`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-06-06T06:00:12]
- key: `CALIBRATION_LIVE|decile 0.00-0.05: n=16 pred=0.0095 actual=0.0625 gap=-0.0530`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-06-06T06:00:12]
- key: `CALIBRATION_LIVE|decile 0.10-0.15: n=6 pred=0.1265 actual=0.1667 gap=-0.0402`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### 🟡 ORPHAN_SCAN  ×1  [2026-06-06T06:00:12]
- key: `ORPHAN_SCAN|209 件の scan に final/retreat 追従無し`
- **FIX**: scan 後 final も retreat も無い→当該レースの final 窓が短すぎ/fetch 失敗

### ℹ️ DRIFT_BUCKET  ×1  [2026-06-06T06:00:12]
- key: `DRIFT_BUCKET|drift ≤-30%: n=42 hit%=31.0% ROI=0.87 (コスト 12,200/回収 10,590)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ CALIBRATION_LIVE  ×1  [2026-06-06T06:00:12]
- key: `CALIBRATION_LIVE|decile 0.20-0.30: n=6 pred=0.2216 actual=0.5000 gap=-0.2784`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-06-06T06:00:12]
- key: `CALIBRATION_LIVE|decile 0.30-0.40: n=24 pred=0.3197 actual=0.2500 gap=+0.0697`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-06-06T06:00:12]
- key: `ROI_STAT|S00: n=154 hit%=27.9% hit_CI[Bonf]=[18.8,39.3]% ROI=0.84 ROI_boot95=[0.60,1.12]`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-06-06T06:00:12]
- key: `INSUFFICIENT_SAMPLE|S00: n=154<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ ROI_STAT  ×1  [2026-06-06T06:00:12]
- key: `ROI_STAT|S01_NAKAANA1: n=129 hit%=29.5% hit_CI[Bonf]=[19.4,42.0]% ROI=0.74 ROI_boot95=[0.`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-06-06T06:00:12]
- key: `INSUFFICIENT_SAMPLE|S01_NAKAANA1: n=129<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留


以下、詳細セクション（通常読み飛ばし可）

## 環境・コード状態
- git_sha: `<error: Command '['git', '-C', '/opt/boa` dirty=True
- config.json md5: `eb532e851a30cd2f7e69bdf0dfca3f2b`
- strategies.json md5: `06b22dd935785e7947bf9c0f170b69a3`
- numpy=2.4.4 lightgbm=4.6.0 scipy=1.17.1
- **calibration_applied**: True ← predictor.py が校正を呼んでるか
- DB: 4.43MB / last modified 2026-06-06T12:30:04.156080+09:00

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
 predictor: Models loaded OK
2026-06-06 12:27:17,293 [WARNING] scraper: beforeinfo parse failed: jcd=03 rno=4
2026-06-06 12:27:17,293 [WARNING] run_cycle: fetch None: 03/4
2026-06-06 12:27:17,293 [INFO] run_cycle: run_cycle done: 0 notifications
2026-06-06 12:28:05,937 [INFO] run_cycle: === run_cycle 12:28:05 ===
2026-06-06 12:28:05,937 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-06-06 12:28:05,937 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-06-06 12:28:05,983 [INFO] predictor: Models loaded OK
2026-06-06 12:28:17,541 [INFO] scraper: odds3t: 120/120 parsed
2026-06-06 12:28:18,745 [INFO] scraper: odds3f: 20/20 parsed
2026-06-06 12:28:19,889 [INFO] scraper: odds2t: 30/30 parsed
2026-06-06 12:28:19,890 [INFO] scraper: odds2f: 15/15 parsed
2026-06-06 12:28:21,008 [INFO] scraper: odds_win: 4/6 parsed
2026-06-06 12:28:21,009 [INFO] scraper: fetch_race 03/4: boats=6 odds=189/191
2026-06-06 12:28:21,020 [INFO] predictor: CALIBRATION_MODE=on
2026-06-06 12:28:21,021 [INFO] predictor: combos: {'win': 4, '2t': 30, '3t': 120}
2026-06-06 12:28:21,028 [INFO] run_cycle: fetched 03/4 [scan]: 154 combos
2026-06-06 12:28:21,085 [INFO] race_id: notif: nid=2026060603041235 sid=S02_TETSUBAN phase=scan rank=B
2026-06-06 12:28:21,628 [INFO] notifier: Discord notify OK (status=204)
2026-06-06 12:28:22,204 [INFO] notifier: Discord notify OK (status=204)
2026-06-06 12:28:22,208 [INFO] run_cycle: SCAN S02_TETSUBAN 江戸川4R B
2026-06-06 12:28:22,310 [INFO] run_cycle: run_cycle done: 1 notifications
2026-06-06 12:29:05,459 [INFO] run_cycle: === run_cycle 12:29:05 ===
2026-06-06 12:29:05,459 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-06-06 12:29:05,459 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-06-06 12:29:05,530 [INFO] predictor: Models loaded OK
2026-06-06 12:29:05,729 [INFO] run_cycle: run_cycle done: 0 notifications

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
    "c": 60
  },
  {
    "target": "primary",
    "ok": 1,
    "c": 60
  }
]
```

## Phase別通知記録 (24h)
{'final': 23, 'result': 14, 'scan': 23}

## アラート件数 (24h・種類別)
```
  ANOMALY_SCRAPER_FAILURE_BURST: 236
  CIRCUIT_BREAKER_TRIP: 63
  CIRCUIT_BREAKER_NO_ACTION: 51
  FINAL_MISSING: 27
  STRATEGY_CI_FAIL: 17
  ANOMALY_SCAN_FINAL_RATIO: 12
  LARGE_ODDS_DRIFT: 2
  ANOMALY_BET_VOLUME_DROP: 1
```

## 戦略別 ROI (7日)
| sid | n | hits | cost | payout | PL | ROI |
|---|---|---|---|---|---|---|
| S00 | 27 | 6 | 8,100 | 3,180 | -4,920 | 0.393 |
| S01_NAKAANA1 | 28 | 7 | 5,600 | 2,920 | -2,680 | 0.521 |
| S02_TETSUBAN | 24 | 6 | 4,800 | 1,640 | -3,160 | 0.342 |

## 直近アラート (24h・新しい順)
```
[12:19:29] ANOMALY_SCAN_FINAL_RATIO: {"abs_drop": -0.154, "baseline_mean": 0.846, "baseline_stdev": 0.058, "kind": "ANOMALY_SCAN_FINAL_RATIO", "today_ratio": 1.0, "today_scan_count": 6, "z_score": 2.67}
[12:09:53] ANOMALY_SCAN_FINAL_RATIO: {"abs_drop": 0.179, "baseline_mean": 0.846, "baseline_stdev": 0.058, "kind": "ANOMALY_SCAN_FINAL_RATIO", "today_ratio": 0.667, "today_scan_count": 6, "z_score": -3.11}
[12:04:46] CIRCUIT_BREAKER_TRIP: {"cost": 8400, "kind": "CIRCUIT_BREAKER_TRIP", "n": 28, "payout": 3180, "roi_7d": 0.379, "sid": "S00"}
[12:02:29] STRATEGY_CI_FAIL: {"ci_lo": null, "kind": "STRATEGY_CI_FAIL", "sid": "S02_TETSUBAN"}
[12:02:29] CIRCUIT_BREAKER_NO_ACTION: {"kind": "CIRCUIT_BREAKER_NO_ACTION", "sid": "S02_TETSUBAN"}
[12:02:29] CIRCUIT_BREAKER_NO_ACTION: {"kind": "CIRCUIT_BREAKER_NO_ACTION", "sid": "S01_NAKAANA1"}
[12:02:29] CIRCUIT_BREAKER_NO_ACTION: {"kind": "CIRCUIT_BREAKER_NO_ACTION", "sid": "S00"}
[11:56:32] ANOMALY_SCAN_FINAL_RATIO: {"abs_drop": -0.154, "baseline_mean": 0.846, "baseline_stdev": 0.058, "kind": "ANOMALY_SCAN_FINAL_RATIO", "today_ratio": 1.0, "today_scan_count": 4, "z_score": 2.67}
[11:51:22] CIRCUIT_BREAKER_TRIP: {"cost": 5800, "kind": "CIRCUIT_BREAKER_TRIP", "n": 29, "payout": 2920, "roi_7d": 0.503, "sid": "S01_NAKAANA1"}
[11:48:22] CIRCUIT_BREAKER_TRIP: {"cost": 5600, "kind": "CIRCUIT_BREAKER_TRIP", "n": 28, "payout": 2920, "roi_7d": 0.521, "sid": "S01_NAKAANA1"}
```

## 本日残レース: 91件

## 本日nidレジャー（ID単位完遂突合せ）
- race_schedule: 132件 登録 / 41件 締切済
- 通知発射: scan=7 nid / final=7 nid / result=4 nid
- predictions: 5 / うち結果DB記録済: 5
- ✅ 結果DBあるが通知未発射: 0件 `tools/backfill_result_notifications.py` で救済可
- ✅ scan後final無しのまま締切: 0件（FINAL_MISSING の温床）

## 直近送信失敗 (24h)
```
```

## 最新 predictions サンプル (計算spot-check用)
| sid | race | bt | combo | p | odds | ev | bet | at |
|---|---|---|---|---|---|---|---|---|
| S01_NAKAANA1 | 108R | win | 1 | 0.4989 | 3.3 | 1.65 | 200 | scan=- drift=- | 11:51:20 |
| S00 | 108R | win | 1 | 0.4989 | 7.8 | 3.89 | 300 | scan=21.0 drift=-62.9% | 11:50:24 |
| S01_NAKAANA1 | 084R | win | 1 | 0.5123 | 3.1 | 1.59 | 200 | scan=- drift=- | 11:48:21 |
| S02_TETSUBAN | 032R | win | 1 | 0.5891 | 2.1 | 1.24 | 200 | scan=- drift=- | 11:38:54 |
| S00 | 083R | win | 1 | 0.4989 | 8.2 | 4.09 | 300 | scan=7.1 drift=+15.5% | 11:22:22 |
| S01_NAKAANA1 | 019R | win | 1 | 0.4111 | 3.6 | 1.48 | 200 | scan=4.9 drift=-26.5% | 19:15:22 |
| S00 | 204R | win | 1 | 0.5123 | 10.4 | 5.33 | 300 | scan=11.7 drift=-11.1% | 16:58:21 |
| S02_TETSUBAN | 073R | win | 1 | 0.5174 | 2.6 | 1.35 | 200 | scan=2.9 drift=-10.3% | 16:35:21 |
| S02_TETSUBAN | 039R | win | 1 | 0.5735 | 2.2 | 1.26 | 200 | scan=- drift=- | 14:49:21 |
| S01_NAKAANA1 | 1011R | win | 1 | 0.3177 | 4.8 | 1.53 | 200 | scan=- drift=- | 13:25:21 |

## オッズドリフト統計 (7日)

| bt | n | avg | min | max | down10 | collapse(≤-30%) | any_large(≥10%) |
|---|---|---|---|---|---|---|---|
| win | 41 | +12.7% | -62.9% | +432.7% | 13 | 5 | 29 |

## 校正テーブル合格状況

- total: 27 グループ
- passed: 19
- failed: 8 — `2f|4, 2f|5, 3f|2, 3f|3, 3f|4, 3t|1, 3t|4, 3t|5`
- 主力グループ状態: ✅ (全12グループ合格)

## SRE Golden Signals (24h)

| Signal | Value |
|---|---|
| **Latency** (scan→final avg) | 465.2s |
| **Latency** (scan→final max) | 651.8s |
| **Traffic** (notifications 24h) | 60 |
| **Errors** (send fail rate) | ✅ 0.0% |
| **Saturation** (S00) | 600円 used |
| **Saturation** (S01_NAKAANA1) | 400円 used |
| **Saturation** (S02_TETSUBAN) | 200円 used |

## 信ぴょう性メトリクス（予測精度の証拠）

### bt別: 予測確率 vs 実的中率
| bt | n | 予測avg | 実的中率 | 校正誤差 | 過信度 | Brier |
|---|---|---|---|---|---|---|
| 3t | 12 | 0.0019 | 0.0833 | -0.0814 | ✅-4200% | 0.0819 |
| win | 361 | 0.4646 | 0.3102 | +0.1543 | 🟡+33% | 0.2382 |

### 戦略別: 校正精度 + Brier Skill Score
| sid | bt | n | pred | actual | Brier | BSS | ROI |
|---|---|---|---|---|---|---|---|
| S00 | win | 155 | 0.4204 | 0.2774 | 0.2234 | 🔴-0.11 | 0.832 |
| S01_NAKAANA1 | win | 131 | 0.4840 | 0.2901 | 0.2429 | 🔴-0.18 | 0.724 |
| S02_TETSUBAN | win | 75 | 0.5220 | 0.4133 | 0.2605 | 🔴-0.07 | 0.744 |
| S04_SELL_3T | 3t | 12 | 0.0019 | 0.0833 | 0.0819 | 🔴-0.07 | 0.617 |

### 確率デシル別: 校正カーブ
| 確率帯 | n | 予測avg | 実的中率 | gap |
|---|---|---|---|---|
| 0.00-0.05 | 16 | 0.0095 | 0.0625 | 🔴-0.0530 |
| 0.10-0.15 | 6 | 0.1265 | 0.1667 | ✅-0.0402 |
| 0.15-0.20 | 6 | 0.1957 | 0.1667 | ✅+0.0291 |
| 0.20-0.30 | 6 | 0.2216 | 0.5000 | 🔴-0.2784 |
| 0.30-0.50 | 146 | 0.4194 | 0.2603 | 🔴+0.1591 |
| 0.50+ | 190 | 0.5413 | 0.3632 | 🔴+0.1782 |

## Settlement Ratio データ品質

- 学習済み: 4バンド / fallback: 13バンド
| bt | odds帯 | source | n | ratio |
|---|---|---|---|---|
| win | <3.0 | ✅learned | 31 | 0.746 |
| win | <5.0 | ✅learned | 58 | 0.737 |
| win | <10.0 | ✅learned | 39 | 0.52 |
| win | <20.0 | ✅learned | 12 | 0.197 |
| win | <50.0 | ⚠️fallback | 1 | 0.1 |
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
_auto-generated by claude_snapshot.py at 2026-06-06T12:30:02.236379+09:00_