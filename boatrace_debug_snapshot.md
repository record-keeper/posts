# ClaudeDebug スナップショット

## 🔴 現状: RED

**生成**: 2026-06-24T15:30:01.743927+09:00

### 次に取るべきアクション
> RED最優先: CIRCUIT_BREAKER_TRIP×43 (24h) → ログ/DB確認

### 検出された問題
- 🔴 CIRCUIT_BREAKER_TRIP×43 (24h)
- 🟡 FINAL_MISSING×33 (24h)
- 🔴 STRATEGY_CI_FAIL×17 (24h)
- 🟡 LARGE_ODDS_DRIFT×1 (24h)
- 🔴 alert_manager dispatch 失敗確定 1件（手動確認必要）

---

## 🔧 AI デバッグキュー（このClaudeが対処）

### 🔴 CIRCUIT_BREAKER_TRIP  ×44  [2026-06-24T15:06:40]
- key: `CIRCUIT_BREAKER_TRIP|`
- **FIX**: 7日ROI<0.7→戦略を enabled:false にして原因調査。校正ドリフトか市場変化を確認

### 🔴 CIRCUIT_BREAKER_NO_ACTION  ×44  [2026-06-24T15:06:40]
- key: `CIRCUIT_BREAKER_NO_ACTION|`
- **FIX**: CIRCUIT_BREAKER_TRIP 発動済なのに strategies.json で enabled のまま。enabled:false に切替 or 復旧条件満たしたか確認

### 🔴 STRATEGY_CI_FAIL  ×22  [2026-06-24T15:06:40]
- key: `STRATEGY_CI_FAIL|`
- **FIX**: grid戦略のOOS CI下限<1.0→論文基準で赤字リスク。strategies.json確認

### 🟡 ANOMALY_SCRAPER_FAILURE_BURST  ×25  [2026-06-24T15:03:41]
- key: `ANOMALY_SCRAPER_FAILURE_BURST|`
- **FIX**: 直近1h でscraper 3-retry 全敗多発。boatrace.jp 側timeout / IP ban / DDoS

### 🔴 CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION  ×3  [2026-06-24T14:30:04]
- key: `CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION|戦略 S00 が TRIP してるが enabled のまま`
- **FIX**: CIRCUIT_BREAKER_TRIP 戦略が enabled のまま。enabled:false に

### 🔴 CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION  ×3  [2026-06-24T14:30:04]
- key: `CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION|戦略 S01_NAKAANA1 が TRIP してるが enabled のまま`
- **FIX**: CIRCUIT_BREAKER_TRIP 戦略が enabled のまま。enabled:false に

### 🟡 ANOMALY_SCAN_FINAL_RATIO  ×8  [2026-06-24T14:07:53]
- key: `ANOMALY_SCAN_FINAL_RATIO|`
- **FIX**: scan→final成立率が7日baselineから2σ逸脱。scan/final window設定・odds取得タイミング

### 🟡 KS_ODDS_DRIFT  ×22  [2026-06-24T13:04:57]
- key: `KS_ODDS_DRIFT|`
- **FIX**: オッズ分布の KS 検定 p<0.01→市場構造変化の可能性。settlement_ratio の fallback 値を再検証

### 🟡 ANOMALY_BET_VOLUME_DROP  ×1  [2026-06-24T13:03:27]
- key: `ANOMALY_BET_VOLUME_DROP|`
- **FIX**: 本日のbet数が7日baselineから2σ低下。戦略filter/ scan fix/run_cycle停止を疑え

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-06-24T06:00:11]
- key: `INSUFFICIENT_SAMPLE|S00: n=156<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-06-24T06:00:11]
- key: `INSUFFICIENT_SAMPLE|S02_TETSUBAN: n=77<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-06-24T06:00:11]
- key: `INSUFFICIENT_SAMPLE|S01_NAKAANA1: n=136<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ CALIBRATION_LIVE  ×1  [2026-06-24T06:00:11]
- key: `CALIBRATION_LIVE|decile 0.05-0.10: n=5 pred=0.0816 actual=0.0000 gap=+0.0816`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### 🟡 ORPHAN_SCAN  ×1  [2026-06-24T06:00:11]
- key: `ORPHAN_SCAN|156 件の scan に final/retreat 追従無し`
- **FIX**: scan 後 final も retreat も無い→当該レースの final 窓が短すぎ/fetch 失敗

### ℹ️ CALIBRATION_LIVE  ×1  [2026-06-24T06:00:11]
- key: `CALIBRATION_LIVE|decile 0.30-0.40: n=21 pred=0.3217 actual=0.2381 gap=+0.0837`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-06-24T06:00:11]
- key: `ROI_STAT|S00: n=156 hit%=25.6% hit_CI[Bonf]=[17.0,36.8]% ROI=0.68 ROI_boot95=[0.48,0.89]`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-06-24T06:00:11]
- key: `ROI_STAT|S01_NAKAANA1: n=136 hit%=30.1% hit_CI[Bonf]=[20.2,42.4]% ROI=0.81 ROI_boot95=[0.`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-06-24T06:00:11]
- key: `ROI_STAT|S02_TETSUBAN: n=77 hit%=33.8% hit_CI[Bonf]=[20.5,50.2]% ROI=0.57 ROI_boot95=[0.3`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ DRIFT_BUCKET  ×1  [2026-06-24T06:00:11]
- key: `DRIFT_BUCKET|drift ≤-30%: n=32 hit%=21.9% ROI=0.72 (コスト 9,100/回収 6,510)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-06-24T06:00:11]
- key: `DRIFT_BUCKET|drift -30%〜-10%: n=34 hit%=23.5% ROI=0.52 (コスト 7,900/回収 4,110)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料


以下、詳細セクション（通常読み飛ばし可）

## 環境・コード状態
- git_sha: `<error: Command '['git', '-C', '/opt/boa` dirty=True
- config.json md5: `eb532e851a30cd2f7e69bdf0dfca3f2b`
- strategies.json md5: `06b22dd935785e7947bf9c0f170b69a3`
- numpy=2.4.4 lightgbm=4.6.0 scipy=1.17.1
- **calibration_applied**: True ← predictor.py が校正を呼んでるか
- DB: 5.86MB / last modified 2026-06-24T15:30:04.583926+09:00

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
2026-06-24 15:28:20,938 [INFO] run_cycle: run_cycle done: 2 notifications
2026-06-24 15:29:04,187 [INFO] run_cycle: === run_cycle 15:29:04 ===
2026-06-24 15:29:04,187 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-06-24 15:29:04,187 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-06-24 15:29:04,247 [INFO] predictor: Models loaded OK
2026-06-24 15:29:16,895 [INFO] scraper: odds3t: 120/120 parsed
2026-06-24 15:29:18,032 [INFO] scraper: odds3f: 20/20 parsed
2026-06-24 15:29:19,165 [INFO] scraper: odds2t: 30/30 parsed
2026-06-24 15:29:19,166 [INFO] scraper: odds2f: 14/15 parsed
2026-06-24 15:29:20,281 [INFO] scraper: odds_win: 5/6 parsed
2026-06-24 15:29:20,281 [INFO] scraper: fetch_race 04/8: boats=6 odds=189/191
2026-06-24 15:29:20,294 [INFO] predictor: CALIBRATION_MODE=on
2026-06-24 15:29:20,294 [INFO] predictor: combos: {'win': 5, '2t': 30, '3t': 120}
2026-06-24 15:29:20,302 [INFO] run_cycle: fetched 04/8 [final]: 155 combos
2026-06-24 15:29:20,638 [INFO] race_id: notif: nid=2026062404081532 sid=S00 phase=final rank=S
2026-06-24 15:29:20,981 [INFO] notifier: Discord notify OK (status=204)
2026-06-24 15:29:21,364 [INFO] notifier: Discord notify OK (status=204)
2026-06-24 15:29:21,466 [INFO] run_cycle: FINAL S00 平和島8R S
2026-06-24 15:29:25,101 [INFO] scraper: odds3t: 120/120 parsed
2026-06-24 15:29:26,260 [INFO] scraper: odds3f: 20/20 parsed
2026-06-24 15:29:27,384 [INFO] scraper: odds2t: 29/30 parsed
2026-06-24 15:29:27,385 [INFO] scraper: odds2f: 14/15 parsed
2026-06-24 15:29:28,482 [INFO] scraper: odds_win: 2/6 parsed
2026-06-24 15:29:28,482 [INFO] scraper: fetch_race 16/10: boats=6 odds=185/191
2026-06-24 15:29:28,490 [INFO] predictor: CALIBRATION_MODE=on
2026-06-24 15:29:28,490 [INFO] predictor: combos: {'win': 2, '2t': 29, '3t': 120}
2026-06-24 15:29:28,498 [INFO] run_cycle: fetched 16/10 [scan]: 151 combos
2026-06-24 15:29:28,615 [INFO] run_cycle: run_cycle done: 1 notifications

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
    "c": 58
  },
  {
    "target": "primary",
    "ok": 1,
    "c": 58
  }
]
```

## Phase別通知記録 (24h)
{'final': 22, 'result': 10, 'scan': 26}

## アラート件数 (24h・種類別)
```
  ANOMALY_SCRAPER_FAILURE_BURST: 151
  CIRCUIT_BREAKER_TRIP: 43
  CIRCUIT_BREAKER_NO_ACTION: 34
  FINAL_MISSING: 33
  STRATEGY_CI_FAIL: 17
  ANOMALY_SCAN_FINAL_RATIO: 5
  ANOMALY_BET_VOLUME_DROP: 4
  KS_ODDS_DRIFT: 2
  LARGE_ODDS_DRIFT: 1
```

## 戦略別 ROI (7日)
| sid | n | hits | cost | payout | PL | ROI |
|---|---|---|---|---|---|---|
| S00 | 47 | 10 | 14,100 | 7,890 | -6,210 | 0.56 |
| S01_NAKAANA1 | 35 | 9 | 7,000 | 4,740 | -2,260 | 0.677 |
| S02_TETSUBAN | 12 | 3 | 2,400 | 1,260 | -1,140 | 0.525 |

## 直近アラート (24h・新しい順)
```
[15:29:28] CIRCUIT_BREAKER_TRIP: {"cost": 14100, "kind": "CIRCUIT_BREAKER_TRIP", "n": 47, "payout": 7890, "roi_7d": 0.56, "sid": "S00"}
[15:29:28] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 4, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1265}
[15:28:20] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 4, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1263}
[15:26:29] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1232}
[15:25:36] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1225}
[15:24:01] CIRCUIT_BREAKER_TRIP: {"cost": 13800, "kind": "CIRCUIT_BREAKER_TRIP", "n": 46, "payout": 7890, "roi_7d": 0.572, "sid": "S00"}
[15:24:01] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1212}
[15:22:32] CIRCUIT_BREAKER_TRIP: {"cost": 7000, "kind": "CIRCUIT_BREAKER_TRIP", "n": 35, "payout": 4740, "roi_7d": 0.677, "sid": "S01_NAKAANA1"}
[15:21:06] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1208}
[15:20:51] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1203}
```

## 本日残レース: 71件

## 本日nidレジャー（ID単位完遂突合せ）
- race_schedule: 180件 登録 / 109件 締切済
- 通知発射: scan=17 nid / final=14 nid / result=5 nid
- predictions: 7 / うち結果DB記録済: 5
- ✅ 結果DBあるが通知未発射: 0件 `tools/backfill_result_notifications.py` で救済可
- 🔴 scan後final無しのまま締切: 2件（FINAL_MISSING の温床）

## 直近送信失敗 (24h)
```
```

## 最新 predictions サンプル (計算spot-check用)
| sid | race | bt | combo | p | odds | ev | bet | at |
|---|---|---|---|---|---|---|---|---|
| S00 | 048R | win | 1 | 0.5476 | 6.7 | 3.67 | 300 | scan=13.2 drift=-49.2% | 15:29:20 |
| S01_NAKAANA1 | 226R | win | 1 | 0.5990 | 3.6 | 2.16 | 200 | scan=3.5 drift=+2.9% | 15:08:20 |
| S00 | 099R | win | 1 | 0.5123 | 4.2 | 2.15 | 300 | scan=5.4 drift=-22.2% | 14:40:25 |
| S00 | 167R | win | 1 | 0.4111 | 8.2 | 3.37 | 300 | scan=6.0 drift=+36.7% | 14:02:23 |
| S00 | 097R | win | 1 | 0.5735 | 4.8 | 2.75 | 300 | scan=4.1 drift=+17.1% | 13:35:22 |
| S01_NAKAANA1 | 036R | win | 1 | 0.5990 | 3.3 | 1.98 | 200 | scan=3.3 drift=+0.0% | 13:26:33 |
| S00 | 096R | win | 1 | 0.5334 | 6.0 | 3.20 | 300 | scan=5.2 drift=+15.4% | 13:04:40 |
| S00 | 078R | win | 1 | 0.4111 | 7.1 | 2.92 | 300 | scan=5.2 drift=+36.5% | 18:54:22 |
| S01_NAKAANA1 | 076R | win | 1 | 0.4111 | 3.1 | 1.27 | 200 | scan=3.0 drift=+3.3% | 18:04:21 |
| S00 | 196R | win | 1 | 0.5174 | 5.3 | 2.74 | 300 | scan=4.5 drift=+17.8% | 17:56:20 |

## オッズドリフト統計 (7日)

| bt | n | avg | min | max | down10 | collapse(≤-30%) | any_large(≥10%) |
|---|---|---|---|---|---|---|---|
| win | 59 | +15.0% | -61.4% | +482.2% | 21 | 8 | 38 |

## 校正テーブル合格状況

- total: 27 グループ
- passed: 19
- failed: 8 — `2f|4, 2f|5, 3f|2, 3f|3, 3f|4, 3t|1, 3t|4, 3t|5`
- 主力グループ状態: ✅ (全12グループ合格)

## SRE Golden Signals (24h)

| Signal | Value |
|---|---|
| **Latency** (scan→final avg) | 483.9s |
| **Latency** (scan→final max) | 602.4s |
| **Traffic** (notifications 24h) | 58 |
| **Errors** (send fail rate) | ✅ 0.0% |
| **Saturation** (S00) | 1,500円 used |
| **Saturation** (S01_NAKAANA1) | 400円 used |

## 信ぴょう性メトリクス（予測精度の証拠）

### bt別: 予測確率 vs 実的中率
| bt | n | 予測avg | 実的中率 | 校正誤差 | 過信度 | Brier |
|---|---|---|---|---|---|---|
| win | 367 | 0.4750 | 0.2888 | +0.1862 | 🟡+39% | 0.2420 |

### 戦略別: 校正精度 + Brier Skill Score
| sid | bt | n | pred | actual | Brier | BSS | ROI |
|---|---|---|---|---|---|---|---|
| S00 | win | 157 | 0.4315 | 0.2548 | 0.2259 | 🔴-0.19 | 0.675 |
| S01_NAKAANA1 | win | 134 | 0.4890 | 0.3060 | 0.2450 | 🔴-0.15 | 0.825 |
| S02_TETSUBAN | win | 76 | 0.5400 | 0.3289 | 0.2698 | 🔴-0.22 | 0.553 |

### 確率デシル別: 校正カーブ
| 確率帯 | n | 予測avg | 実的中率 | gap |
|---|---|---|---|---|
| 0.15-0.20 | 8 | 0.1802 | 0.3750 | 🔴-0.1948 |
| 0.20-0.30 | 12 | 0.2243 | 0.0833 | 🔴+0.1410 |
| 0.30-0.50 | 124 | 0.4216 | 0.2419 | 🔴+0.1797 |
| 0.50+ | 216 | 0.5427 | 0.3287 | 🔴+0.2140 |

## Settlement Ratio データ品質

- 学習済み: 4バンド / fallback: 13バンド
| bt | odds帯 | source | n | ratio |
|---|---|---|---|---|
| win | <3.0 | ✅learned | 46 | 0.733 |
| win | <5.0 | ✅learned | 92 | 0.734 |
| win | <10.0 | ✅learned | 57 | 0.496 |
| win | <20.0 | ✅learned | 15 | 0.207 |
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
_auto-generated by claude_snapshot.py at 2026-06-24T15:30:01.743927+09:00_