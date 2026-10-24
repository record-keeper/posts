# ClaudeDebug スナップショット

## 🔴 現状: RED

**生成**: 2026-10-24T14:40:01.551629+09:00

### 次に取るべきアクション
> RED最優先: CIRCUIT_BREAKER_TRIP×50 (24h) → ログ/DB確認

### 検出された問題
- 🟡 FINAL_MISSING×83 (24h)
- 🔴 CIRCUIT_BREAKER_TRIP×50 (24h)
- 🔴 STRATEGY_CI_FAIL×17 (24h)
- 🟡 LARGE_ODDS_DRIFT×2 (24h)
- 🔴 alert_manager dispatch 失敗確定 1件（手動確認必要）

---

## 🔧 AI デバッグキュー（このClaudeが対処）

### 🔴 CIRCUIT_BREAKER_TRIP  ×74  [2026-10-24T14:02:30]
- key: `CIRCUIT_BREAKER_TRIP|`
- **FIX**: 7日ROI<0.7→戦略を enabled:false にして原因調査。校正ドリフトか市場変化を確認

### 🔴 CIRCUIT_BREAKER_NO_ACTION  ×74  [2026-10-24T14:02:30]
- key: `CIRCUIT_BREAKER_NO_ACTION|`
- **FIX**: CIRCUIT_BREAKER_TRIP 発動済なのに strategies.json で enabled のまま。enabled:false に切替 or 復旧条件満たしたか確認

### 🔴 STRATEGY_CI_FAIL  ×37  [2026-10-24T14:02:30]
- key: `STRATEGY_CI_FAIL|`
- **FIX**: grid戦略のOOS CI下限<1.0→論文基準で赤字リスク。strategies.json確認

### 🔴 CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION  ×2  [2026-10-24T14:00:03]
- key: `CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION|戦略 S00 が TRIP してるが enabled のまま`
- **FIX**: CIRCUIT_BREAKER_TRIP 戦略が enabled のまま。enabled:false に

### 🔴 CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION  ×2  [2026-10-24T14:00:03]
- key: `CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION|戦略 S01_NAKAANA1 が TRIP してるが enabled のまま`
- **FIX**: CIRCUIT_BREAKER_TRIP 戦略が enabled のまま。enabled:false に

### 🟡 ANOMALY_SCRAPER_FAILURE_BURST  ×56  [2026-10-24T13:42:40]
- key: `ANOMALY_SCRAPER_FAILURE_BURST|`
- **FIX**: 直近1h でscraper 3-retry 全敗多発。boatrace.jp 側timeout / IP ban / DDoS

### 🟡 ANOMALY_SCAN_FINAL_RATIO  ×10  [2026-10-24T13:27:21]
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


以下、詳細セクション（通常読み飛ばし可）

## 環境・コード状態
- git_sha: `<error: Command '['git', '-C', '/opt/boa` dirty=True
- config.json md5: `eb532e851a30cd2f7e69bdf0dfca3f2b`
- strategies.json md5: `06b22dd935785e7947bf9c0f170b69a3`
- numpy=2.4.4 lightgbm=4.6.0 scipy=1.17.1
- **calibration_applied**: True ← predictor.py が校正を呼んでるか
- DB: 16.68MB / last modified 2026-10-24T14:39:20.740860+09:00

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
24,615 [INFO] scraper: odds3t: 120/120 parsed
2026-10-24 14:38:25,791 [INFO] scraper: odds3f: 20/20 parsed
2026-10-24 14:38:27,009 [INFO] scraper: odds2t: 29/30 parsed
2026-10-24 14:38:27,010 [INFO] scraper: odds2f: 15/15 parsed
2026-10-24 14:38:28,144 [INFO] scraper: odds_win: 4/6 parsed
2026-10-24 14:38:28,144 [INFO] scraper: fetch_race 05/10: boats=6 odds=188/191
2026-10-24 14:38:28,146 [INFO] predictor: CALIBRATION_MODE=on
2026-10-24 14:38:28,147 [INFO] predictor: combos: {'win': 4, '2t': 29, '3t': 120}
2026-10-24 14:38:28,150 [INFO] run_cycle: fetched 05/10 [scan]: 153 combos
2026-10-24 14:38:28,584 [INFO] race_id: notif: nid=2026102405101451 sid=S02_TETSUBAN phase=scan rank=B
2026-10-24 14:38:28,985 [INFO] notifier: Discord notify OK (status=204)
2026-10-24 14:38:29,656 [INFO] notifier: Discord notify OK (status=204)
2026-10-24 14:38:29,853 [INFO] run_cycle: SCAN S02_TETSUBAN 多摩川10R B
2026-10-24 14:38:29,962 [INFO] run_cycle: run_cycle done: 2 notifications
2026-10-24 14:39:04,252 [INFO] run_cycle: === run_cycle 14:39:04 ===
2026-10-24 14:39:04,252 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-10-24 14:39:04,252 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-10-24 14:39:04,280 [INFO] predictor: Models loaded OK
2026-10-24 14:39:16,786 [INFO] scraper: odds3t: 120/120 parsed
2026-10-24 14:39:17,890 [INFO] scraper: odds3f: 20/20 parsed
2026-10-24 14:39:18,971 [INFO] scraper: odds2t: 30/30 parsed
2026-10-24 14:39:18,972 [INFO] scraper: odds2f: 15/15 parsed
2026-10-24 14:39:20,046 [INFO] scraper: odds_win: 6/6 parsed
2026-10-24 14:39:20,046 [INFO] scraper: fetch_race 04/9: boats=6 odds=191/191
2026-10-24 14:39:20,049 [INFO] predictor: CALIBRATION_MODE=on
2026-10-24 14:39:20,049 [INFO] predictor: combos: {'win': 6, '2t': 30, '3t': 120}
2026-10-24 14:39:20,053 [INFO] run_cycle: fetched 04/9 [final]: 156 combos
2026-10-24 14:39:20,441 [INFO] run_cycle: run_cycle done: 0 notifications

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
    "c": 72
  },
  {
    "target": "primary",
    "ok": 1,
    "c": 72
  }
]
```

## Phase別通知記録 (24h)
{'final': 29, 'result': 19, 'scan': 24}

## アラート件数 (24h・種類別)
```
  ANOMALY_SCRAPER_FAILURE_BURST: 199
  FINAL_MISSING: 83
  CIRCUIT_BREAKER_TRIP: 50
  CIRCUIT_BREAKER_NO_ACTION: 34
  ANOMALY_SCAN_FINAL_RATIO: 20
  STRATEGY_CI_FAIL: 17
  LARGE_ODDS_DRIFT: 2
```

## 戦略別 ROI (7日)
| sid | n | hits | cost | payout | PL | ROI |
|---|---|---|---|---|---|---|
| S00 | 42 | 11 | 12,600 | 8,520 | -4,080 | 0.676 |
| S01_NAKAANA1 | 53 | 11 | 10,600 | 4,680 | -5,920 | 0.442 |
| S02_TETSUBAN | 12 | 6 | 2,400 | 2,540 | +140 | 1.058 |

## 直近アラート (24h・新しい順)
```
[14:38:30] CIRCUIT_BREAKER_TRIP: {"cost": 12600, "kind": "CIRCUIT_BREAKER_TRIP", "n": 42, "payout": 8520, "roi_7d": 0.676, "sid": "S00"}
[14:38:30] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 4, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1228}
[14:37:19] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 4, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1239}
[14:36:20] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 4, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1243}
[14:35:20] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 4, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1258}
[14:33:31] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 4, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1251}
[14:32:19] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 4, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1286}
[14:31:34] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 4, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1278}
[14:30:28] FINAL_MISSING: {"deadline": "2026-10-24T12:59:00+09:00", "kind": "FINAL_MISSING", "nid": "2026102422051259", "sid": "S00"}
[14:29:04] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 4, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1274}
```

## 本日残レース: 61件

## 本日nidレジャー（ID単位完遂突合せ）
- race_schedule: 168件 登録 / 107件 締切済
- 通知発射: scan=17 nid / final=18 nid / result=12 nid
- predictions: 15 / うち結果DB記録済: 14
- ✅ 結果DBあるが通知未発射: 0件 `tools/backfill_result_notifications.py` で救済可
- 🔴 scan後final無しのまま締切: 4件（FINAL_MISSING の温床）

## 直近送信失敗 (24h)
```
```

## 最新 predictions サンプル (計算spot-check用)
| sid | race | bt | combo | p | odds | ev | bet | at |
|---|---|---|---|---|---|---|---|---|
| S00 | 049R | win | 1 | 0.5735 | 7.9 | 4.53 | 300 | scan=8.2 drift=-3.7% | 14:38:19 |
| S01_NAKAANA1 | 098R | win | 1 | 0.5334 | 4.7 | 2.51 | 200 | scan=- drift=- | 13:53:24 |
| S00 | 098R | win | 1 | 0.5334 | 4.7 | 2.51 | 300 | scan=- drift=- | 13:53:19 |
| S01_NAKAANA1 | 1011R | win | 1 | 0.5123 | 3.3 | 1.69 | 200 | scan=- drift=- | 13:47:20 |
| S00 | 046R | win | 1 | 0.3177 | 5.1 | 1.62 | 300 | scan=- drift=- | 13:11:31 |
| S00 | 096R | win | 1 | 0.5334 | 6.7 | 3.57 | 300 | scan=- drift=- | 12:49:20 |
| S00 | 134R | win | 1 | 0.5123 | 4.5 | 2.31 | 300 | scan=- drift=- | 12:12:21 |
| S00 | 115R | win | 1 | 0.4111 | 6.7 | 2.75 | 300 | scan=- drift=- | 12:10:23 |
| S00 | 108R | win | 1 | 0.5174 | 4.7 | 2.43 | 300 | scan=- drift=- | 12:08:30 |
| S00 | 133R | win | 1 | 0.5891 | 6.5 | 3.83 | 300 | scan=- drift=- | 11:38:19 |

## オッズドリフト統計 (7日)

| bt | n | avg | min | max | down10 | collapse(≤-30%) | any_large(≥10%) |
|---|---|---|---|---|---|---|---|
| win | 59 | +28.5% | -52.3% | +495.8% | 8 | 2 | 35 |

## 校正テーブル合格状況

- total: 27 グループ
- passed: 19
- failed: 8 — `2f|4, 2f|5, 3f|2, 3f|3, 3f|4, 3t|1, 3t|4, 3t|5`
- 主力グループ状態: ✅ (全12グループ合格)

## SRE Golden Signals (24h)

| Signal | Value |
|---|---|
| **Latency** (scan→final avg) | 466.9s |
| **Latency** (scan→final max) | 600.3s |
| **Traffic** (notifications 24h) | 72 |
| **Errors** (send fail rate) | ✅ 0.0% |
| **Saturation** (S00) | 3,300円 used |
| **Saturation** (S01_NAKAANA1) | 800円 used |

## 信ぴょう性メトリクス（予測精度の証拠）

### bt別: 予測確率 vs 実的中率
| bt | n | 予測avg | 実的中率 | 校正誤差 | 過信度 | Brier |
|---|---|---|---|---|---|---|
| win | 455 | 0.4790 | 0.3495 | +0.1295 | 🟡+27% | 0.2418 |

### 戦略別: 校正精度 + Brier Skill Score
| sid | bt | n | pred | actual | Brier | BSS | ROI |
|---|---|---|---|---|---|---|---|
| S00 | win | 185 | 0.4389 | 0.2973 | 0.2350 | 🔴-0.12 | 0.807 |
| S01_NAKAANA1 | win | 193 | 0.4917 | 0.3316 | 0.2422 | 🔴-0.09 | 0.906 |
| S02_TETSUBAN | win | 77 | 0.5432 | 0.5195 | 0.2571 | 🔴-0.03 | 0.955 |

### 確率デシル別: 校正カーブ
| 確率帯 | n | 予測avg | 実的中率 | gap |
|---|---|---|---|---|
| 0.10-0.15 | 6 | 0.1269 | 0.3333 | 🔴-0.2064 |
| 0.15-0.20 | 8 | 0.1854 | 0.0000 | 🔴+0.1854 |
| 0.20-0.30 | 8 | 0.2288 | 0.2500 | ✅-0.0212 |
| 0.30-0.50 | 158 | 0.4122 | 0.3101 | 🔴+0.1021 |
| 0.50+ | 274 | 0.5425 | 0.3832 | 🔴+0.1593 |

## Settlement Ratio データ品質

- 学習済み: 4バンド / fallback: 13バンド
| bt | odds帯 | source | n | ratio |
|---|---|---|---|---|
| win | <3.0 | ✅learned | 192 | 0.781 |
| win | <5.0 | ✅learned | 346 | 0.745 |
| win | <10.0 | ✅learned | 153 | 0.454 |
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
_auto-generated by claude_snapshot.py at 2026-10-24T14:40:01.551629+09:00_