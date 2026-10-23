# ClaudeDebug スナップショット

## 🔴 現状: RED

**生成**: 2026-10-23T13:10:01.293049+09:00

### 次に取るべきアクション
> RED最優先: CIRCUIT_BREAKER_TRIP×43 (24h) → ログ/DB確認

### 検出された問題
- 🟡 FINAL_MISSING×72 (24h)
- 🔴 CIRCUIT_BREAKER_TRIP×43 (24h)
- 🔴 STRATEGY_CI_FAIL×17 (24h)
- 🔴 SEND_WITHOUT_DBREC×1 (24h)
- 🔴 alert_manager dispatch 失敗確定 1件（手動確認必要）

---

## 🔧 AI デバッグキュー（このClaudeが対処）

### 🟡 ANOMALY_SCRAPER_FAILURE_BURST  ×5  [2026-10-23T13:05:56]
- key: `ANOMALY_SCRAPER_FAILURE_BURST|`
- **FIX**: 直近1h でscraper 3-retry 全敗多発。boatrace.jp 側timeout / IP ban / DDoS

### 🔴 CIRCUIT_BREAKER_TRIP  ×12  [2026-10-23T13:04:28]
- key: `CIRCUIT_BREAKER_TRIP|`
- **FIX**: 7日ROI<0.7→戦略を enabled:false にして原因調査。校正ドリフトか市場変化を確認

### 🔴 CIRCUIT_BREAKER_NO_ACTION  ×12  [2026-10-23T13:04:28]
- key: `CIRCUIT_BREAKER_NO_ACTION|`
- **FIX**: CIRCUIT_BREAKER_TRIP 発動済なのに strategies.json で enabled のまま。enabled:false に切替 or 復旧条件満たしたか確認

### 🔴 STRATEGY_CI_FAIL  ×6  [2026-10-23T13:04:28]
- key: `STRATEGY_CI_FAIL|`
- **FIX**: grid戦略のOOS CI下限<1.0→論文基準で赤字リスク。strategies.json確認

### 🟡 ANOMALY_SCAN_FINAL_RATIO  ×28  [2026-10-23T12:30:47]
- key: `ANOMALY_SCAN_FINAL_RATIO|`
- **FIX**: scan→final成立率が7日baselineから2σ逸脱。scan/final window設定・odds取得タイミング

### 🔴 CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION  ×2  [2026-10-23T12:30:03]
- key: `CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION|戦略 S00 が TRIP してるが enabled のまま`
- **FIX**: CIRCUIT_BREAKER_TRIP 戦略が enabled のまま。enabled:false に

### 🔴 CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION  ×2  [2026-10-23T12:30:03]
- key: `CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION|戦略 S01_NAKAANA1 が TRIP してるが enabled のまま`
- **FIX**: CIRCUIT_BREAKER_TRIP 戦略が enabled のまま。enabled:false に

### 🔴 SEND_WITHOUT_DBREC  ×1  [2026-10-23T12:17:38]
- key: `SEND_WITHOUT_DBREC|`
- **FIX**: record_notification の例外→DB書込エラー原因特定（WAL、ロック）

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-10-23T06:00:24]
- key: `INSUFFICIENT_SAMPLE|S02_TETSUBAN: n=82<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-10-23T06:00:24]
- key: `INSUFFICIENT_SAMPLE|S00: n=186<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-10-23T06:00:24]
- key: `INSUFFICIENT_SAMPLE|S01_NAKAANA1: n=182<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ CALIBRATION_LIVE  ×1  [2026-10-23T06:00:24]
- key: `CALIBRATION_LIVE|decile 0.10-0.15: n=6 pred=0.1269 actual=0.3333 gap=-0.2064`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### 🟡 ORPHAN_SCAN  ×1  [2026-10-23T06:00:24]
- key: `ORPHAN_SCAN|153 件の scan に final/retreat 追従無し`
- **FIX**: scan 後 final も retreat も無い→当該レースの final 窓が短すぎ/fetch 失敗

### ℹ️ CALIBRATION_LIVE  ×1  [2026-10-23T06:00:24]
- key: `CALIBRATION_LIVE|decile 0.30-0.40: n=33 pred=0.3210 actual=0.2121 gap=+0.1089`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ DRIFT_BUCKET  ×1  [2026-10-23T06:00:24]
- key: `DRIFT_BUCKET|drift ≥+30%: n=53 hit%=24.5% ROI=0.77 (コスト 13,900/回収 10,660)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ ROI_STAT  ×1  [2026-10-23T06:00:24]
- key: `ROI_STAT|S00: n=186 hit%=28.0% hit_CI[Bonf]=[19.6,38.2]% ROI=0.75 ROI_boot95=[0.55,0.99]`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-10-23T06:00:24]
- key: `ROI_STAT|S01_NAKAANA1: n=182 hit%=34.6% hit_CI[Bonf]=[25.3,45.3]% ROI=0.94 ROI_boot95=[0.`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-10-23T06:00:24]
- key: `ROI_STAT|S02_TETSUBAN: n=82 hit%=51.2% hit_CI[Bonf]=[35.9,66.3]% ROI=0.94 ROI_boot95=[0.7`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ DRIFT_BUCKET  ×1  [2026-10-23T06:00:24]
- key: `DRIFT_BUCKET|drift ≤-30%: n=29 hit%=44.8% ROI=1.15 (コスト 8,400/回収 9,630)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-10-23T06:00:24]
- key: `DRIFT_BUCKET|drift -30%〜-10%: n=46 hit%=34.8% ROI=0.74 (コスト 11,000/回収 8,120)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料


以下、詳細セクション（通常読み飛ばし可）

## 環境・コード状態
- git_sha: `<error: Command '['git', '-C', '/opt/boa` dirty=True
- config.json md5: `eb532e851a30cd2f7e69bdf0dfca3f2b`
- strategies.json md5: `06b22dd935785e7947bf9c0f170b69a3`
- numpy=2.4.4 lightgbm=4.6.0 scipy=1.17.1
- **calibration_applied**: True ← predictor.py が校正を呼んでるか
- DB: 16.51MB / last modified 2026-10-23T13:09:27.131206+09:00

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
an]: 155 combos
2026-10-23 13:08:38,871 [INFO] run_cycle: run_cycle done: 0 notifications
2026-10-23 13:09:04,255 [INFO] run_cycle: === run_cycle 13:09:04 ===
2026-10-23 13:09:04,255 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-10-23 13:09:04,255 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-10-23 13:09:04,283 [INFO] predictor: Models loaded OK
2026-10-23 13:09:15,764 [INFO] scraper: odds3t: 120/120 parsed
2026-10-23 13:09:16,843 [INFO] scraper: odds3f: 20/20 parsed
2026-10-23 13:09:17,934 [INFO] scraper: odds2t: 30/30 parsed
2026-10-23 13:09:17,935 [INFO] scraper: odds2f: 12/15 parsed
2026-10-23 13:09:19,008 [INFO] scraper: odds_win: 5/6 parsed
2026-10-23 13:09:19,008 [INFO] scraper: fetch_race 17/7: boats=6 odds=187/191
2026-10-23 13:09:19,011 [INFO] predictor: CALIBRATION_MODE=on
2026-10-23 13:09:19,011 [INFO] predictor: combos: {'win': 5, '2t': 30, '3t': 120}
2026-10-23 13:09:19,014 [INFO] run_cycle: fetched 17/7 [final]: 155 combos
2026-10-23 13:09:22,524 [INFO] scraper: odds3t: 120/120 parsed
2026-10-23 13:09:23,596 [INFO] scraper: odds3f: 20/20 parsed
2026-10-23 13:09:24,715 [INFO] scraper: odds2t: 29/30 parsed
2026-10-23 13:09:24,716 [INFO] scraper: odds2f: 12/15 parsed
2026-10-23 13:09:25,805 [INFO] scraper: odds_win: 4/6 parsed
2026-10-23 13:09:25,805 [INFO] scraper: fetch_race 11/7: boats=6 odds=185/191
2026-10-23 13:09:25,808 [INFO] predictor: CALIBRATION_MODE=on
2026-10-23 13:09:25,808 [INFO] predictor: combos: {'win': 4, '2t': 29, '3t': 120}
2026-10-23 13:09:25,811 [INFO] run_cycle: fetched 11/7 [scan]: 153 combos
2026-10-23 13:09:26,170 [INFO] run_cycle: run_cycle done: 0 notifications
2026-10-23 13:10:05,502 [INFO] run_cycle: === run_cycle 13:10:05 ===
2026-10-23 13:10:05,502 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-10-23 13:10:05,502 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000

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
    "c": 62
  },
  {
    "target": "primary",
    "ok": 1,
    "c": 62
  }
]
```

## Phase別通知記録 (24h)
{'final': 24, 'result': 14, 'scan': 24}

## アラート件数 (24h・種類別)
```
  FINAL_MISSING: 72
  ANOMALY_SCRAPER_FAILURE_BURST: 66
  CIRCUIT_BREAKER_TRIP: 43
  CIRCUIT_BREAKER_NO_ACTION: 33
  STRATEGY_CI_FAIL: 17
  ANOMALY_SCAN_FINAL_RATIO: 12
  SEND_WITHOUT_DBREC: 1
```

## 戦略別 ROI (7日)
| sid | n | hits | cost | payout | PL | ROI |
|---|---|---|---|---|---|---|
| S00 | 32 | 8 | 9,600 | 6,450 | -3,150 | 0.672 |
| S01_NAKAANA1 | 48 | 12 | 9,600 | 5,580 | -4,020 | 0.581 |
| S02_TETSUBAN | 14 | 8 | 2,800 | 3,580 | +780 | 1.279 |

## 直近アラート (24h・新しい順)
```
[13:09:26] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1344}
[13:08:38] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1345}
[13:07:05] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1356}
[13:06:45] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1355}
[13:06:45] ANOMALY_SCAN_FINAL_RATIO: {"abs_drop": 0.145, "baseline_mean": 0.845, "baseline_stdev": 0.06, "kind": "ANOMALY_SCAN_FINAL_RATIO", "today_ratio": 0.7, "today_scan_count": 10, "z_score": -2.41}
[13:05:56] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1322}
[13:04:26] STRATEGY_CI_FAIL: {"ci_lo": null, "kind": "STRATEGY_CI_FAIL", "sid": "S02_TETSUBAN"}
[13:04:26] CIRCUIT_BREAKER_NO_ACTION: {"kind": "CIRCUIT_BREAKER_NO_ACTION", "sid": "S01_NAKAANA1"}
[13:04:26] CIRCUIT_BREAKER_NO_ACTION: {"kind": "CIRCUIT_BREAKER_NO_ACTION", "sid": "S00"}
[13:00:45] ANOMALY_SCAN_FINAL_RATIO: {"abs_drop": 0.245, "baseline_mean": 0.845, "baseline_stdev": 0.06, "kind": "ANOMALY_SCAN_FINAL_RATIO", "today_ratio": 0.6, "today_scan_count": 10, "z_score": -4.07}
```

## 本日残レース: 93件

## 本日nidレジャー（ID単位完遂突合せ）
- race_schedule: 168件 登録 / 75件 締切済
- 通知発射: scan=10 nid / final=10 nid / result=3 nid
- predictions: 4 / うち結果DB記録済: 3
- ✅ 結果DBあるが通知未発射: 0件 `tools/backfill_result_notifications.py` で救済可
- 🔴 scan後final無しのまま締切: 4件（FINAL_MISSING の温床）

## 直近送信失敗 (24h)
```
```

## 最新 predictions サンプル (計算spot-check用)
| sid | race | bt | combo | p | odds | ev | bet | at |
|---|---|---|---|---|---|---|---|---|
| S01_NAKAANA1 | 066R | win | 1 | 0.5174 | 3.6 | 1.86 | 200 | scan=- drift=- | 12:55:29 |
| S01_NAKAANA1 | 149R | win | 1 | 0.5476 | 3.1 | 1.70 | 200 | scan=3.0 drift=+3.3% | 12:24:18 |
| S00 | 043R | win | 1 | 0.4111 | 10.2 | 4.19 | 300 | scan=- drift=- | 11:45:41 |
| S01_NAKAANA1 | 173R | win | 1 | 0.4989 | 3.7 | 1.85 | 200 | scan=- drift=- | 11:13:19 |
| S00 | 246R | win | 1 | 0.3177 | 4.0 | 1.27 | 300 | scan=4.2 drift=-4.8% | 17:47:18 |
| S01_NAKAANA1 | 126R | win | 1 | 0.5123 | 4.2 | 2.15 | 200 | scan=3.5 drift=+20.0% | 17:26:18 |
| S01_NAKAANA1 | 122R | win | 1 | 0.4111 | 4.2 | 1.73 | 200 | scan=4.2 drift=+0.0% | 15:37:19 |
| S00 | 1110R | win | 1 | 0.5174 | 8.2 | 4.24 | 300 | scan=4.5 drift=+82.2% | 14:27:27 |
| S01_NAKAANA1 | 068R | win | 1 | 0.4111 | 4.1 | 1.69 | 200 | scan=3.3 drift=+24.2% | 14:04:19 |
| S01_NAKAANA1 | 119R | win | 1 | 0.5228 | 4.5 | 2.35 | 200 | scan=- drift=- | 13:59:20 |

## オッズドリフト統計 (7日)

| bt | n | avg | min | max | down10 | collapse(≤-30%) | any_large(≥10%) |
|---|---|---|---|---|---|---|---|
| win | 57 | +28.7% | -52.3% | +495.8% | 8 | 2 | 34 |

## 校正テーブル合格状況

- total: 27 グループ
- passed: 19
- failed: 8 — `2f|4, 2f|5, 3f|2, 3f|3, 3f|4, 3t|1, 3t|4, 3t|5`
- 主力グループ状態: ✅ (全12グループ合格)

## SRE Golden Signals (24h)

| Signal | Value |
|---|---|
| **Latency** (scan→final avg) | 480.7s |
| **Latency** (scan→final max) | 611.8s |
| **Traffic** (notifications 24h) | 62 |
| **Errors** (send fail rate) | ✅ 0.0% |
| **Saturation** (S00) | 300円 used |
| **Saturation** (S01_NAKAANA1) | 600円 used |

## 信ぴょう性メトリクス（予測精度の証拠）

### bt別: 予測確率 vs 実的中率
| bt | n | 予測avg | 実的中率 | 校正誤差 | 過信度 | Brier |
|---|---|---|---|---|---|---|
| win | 446 | 0.4799 | 0.3520 | +0.1279 | 🟡+27% | 0.2435 |

### 戦略別: 校正精度 + Brier Skill Score
| sid | bt | n | pred | actual | Brier | BSS | ROI |
|---|---|---|---|---|---|---|---|
| S00 | win | 181 | 0.4401 | 0.2873 | 0.2371 | 🔴-0.16 | 0.788 |
| S01_NAKAANA1 | win | 184 | 0.4931 | 0.3424 | 0.2432 | 🔴-0.08 | 0.93 |
| S02_TETSUBAN | win | 81 | 0.5391 | 0.5185 | 0.2583 | 🔴-0.03 | 0.953 |

### 確率デシル別: 校正カーブ
| 確率帯 | n | 予測avg | 実的中率 | gap |
|---|---|---|---|---|
| 0.10-0.15 | 6 | 0.1269 | 0.3333 | 🔴-0.2064 |
| 0.15-0.20 | 8 | 0.1824 | 0.0000 | 🔴+0.1824 |
| 0.20-0.30 | 8 | 0.2288 | 0.2500 | ✅-0.0212 |
| 0.30-0.50 | 155 | 0.4152 | 0.3226 | 🔴+0.0926 |
| 0.50+ | 268 | 0.5431 | 0.3806 | 🔴+0.1625 |

## Settlement Ratio データ品質

- 学習済み: 4バンド / fallback: 13バンド
| bt | odds帯 | source | n | ratio |
|---|---|---|---|---|
| win | <3.0 | ✅learned | 191 | 0.782 |
| win | <5.0 | ✅learned | 343 | 0.746 |
| win | <10.0 | ✅learned | 150 | 0.457 |
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
_auto-generated by claude_snapshot.py at 2026-10-23T13:10:01.293049+09:00_