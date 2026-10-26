# ClaudeDebug スナップショット

## 🔴 現状: RED

**生成**: 2026-10-26T12:50:01.722922+09:00

### 次に取るべきアクション
> RED最優先: CIRCUIT_BREAKER_TRIP×45 (24h) → ログ/DB確認

### 検出された問題
- 🟡 FINAL_MISSING×61 (24h)
- 🔴 CIRCUIT_BREAKER_TRIP×45 (24h)
- 🔴 STRATEGY_CI_FAIL×17 (24h)
- 🔴 alert_manager dispatch 失敗確定 1件（手動確認必要）

---

## 🔧 AI デバッグキュー（このClaudeが対処）

### 🟡 ANOMALY_SCRAPER_FAILURE_BURST  ×16  [2026-10-26T12:34:29]
- key: `ANOMALY_SCRAPER_FAILURE_BURST|`
- **FIX**: 直近1h でscraper 3-retry 全敗多発。boatrace.jp 側timeout / IP ban / DDoS

### 🔴 CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION  ×1  [2026-10-26T12:30:03]
- key: `CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION|戦略 S00 が TRIP してるが enabled のまま`
- **FIX**: CIRCUIT_BREAKER_TRIP 戦略が enabled のまま。enabled:false に

### 🔴 CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION  ×1  [2026-10-26T12:30:03]
- key: `CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION|戦略 S01_NAKAANA1 が TRIP してるが enabled のまま`
- **FIX**: CIRCUIT_BREAKER_TRIP 戦略が enabled のまま。enabled:false に

### 🟡 ANOMALY_SCAN_FINAL_RATIO  ×23  [2026-10-26T12:27:46]
- key: `ANOMALY_SCAN_FINAL_RATIO|`
- **FIX**: scan→final成立率が7日baselineから2σ逸脱。scan/final window設定・odds取得タイミング

### 🔴 CIRCUIT_BREAKER_TRIP  ×94  [2026-10-26T12:03:38]
- key: `CIRCUIT_BREAKER_TRIP|`
- **FIX**: 7日ROI<0.7→戦略を enabled:false にして原因調査。校正ドリフトか市場変化を確認

### 🔴 CIRCUIT_BREAKER_NO_ACTION  ×94  [2026-10-26T12:03:38]
- key: `CIRCUIT_BREAKER_NO_ACTION|`
- **FIX**: CIRCUIT_BREAKER_TRIP 発動済なのに strategies.json で enabled のまま。enabled:false に切替 or 復旧条件満たしたか確認

### 🔴 STRATEGY_CI_FAIL  ×47  [2026-10-26T12:03:38]
- key: `STRATEGY_CI_FAIL|`
- **FIX**: grid戦略のOOS CI下限<1.0→論文基準で赤字リスク。strategies.json確認

### 🟡 ANOMALY_BET_VOLUME_DROP  ×52  [2026-10-26T10:00:12]
- key: `ANOMALY_BET_VOLUME_DROP|`
- **FIX**: 本日のbet数が7日baselineから2σ低下。戦略filter/ scan fix/run_cycle停止を疑え

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-10-26T06:00:39]
- key: `INSUFFICIENT_SAMPLE|S02_TETSUBAN: n=72<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### 🟡 ORPHAN_SCAN  ×1  [2026-10-26T06:00:39]
- key: `ORPHAN_SCAN|163 件の scan に final/retreat 追従無し`
- **FIX**: scan 後 final も retreat も無い→当該レースの final 窓が短すぎ/fetch 失敗

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-10-26T06:00:39]
- key: `INSUFFICIENT_SAMPLE|S00: n=184<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ DRIFT_BUCKET  ×1  [2026-10-26T06:00:39]
- key: `DRIFT_BUCKET|drift +10%〜+30%: n=66 hit%=31.8% ROI=0.83 (コスト 15,700/回収 13,040)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ CALIBRATION_LIVE  ×1  [2026-10-26T06:00:39]
- key: `CALIBRATION_LIVE|decile 0.15-0.20: n=8 pred=0.1854 actual=0.0000 gap=+0.1854`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-10-26T06:00:39]
- key: `ROI_STAT|S00: n=184 hit%=29.9% hit_CI[Bonf]=[21.2,40.3]% ROI=0.80 ROI_boot95=[0.59,1.03]`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-10-26T06:00:39]
- key: `ROI_STAT|S01_NAKAANA1: n=192 hit%=33.9% hit_CI[Bonf]=[24.9,44.2]% ROI=0.90 ROI_boot95=[0.`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-10-26T06:00:39]
- key: `INSUFFICIENT_SAMPLE|S01_NAKAANA1: n=192<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ ROI_STAT  ×1  [2026-10-26T06:00:39]
- key: `ROI_STAT|S02_TETSUBAN: n=72 hit%=51.4% hit_CI[Bonf]=[35.1,67.3]% ROI=0.89 ROI_boot95=[0.6`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ DRIFT_BUCKET  ×1  [2026-10-26T06:00:39]
- key: `DRIFT_BUCKET|drift ≤-30%: n=27 hit%=44.4% ROI=1.17 (コスト 7,800/回収 9,150)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-10-26T06:00:39]
- key: `DRIFT_BUCKET|drift -30%〜-10%: n=45 hit%=31.1% ROI=0.60 (コスト 11,000/回収 6,590)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-10-26T06:00:39]
- key: `DRIFT_BUCKET|drift -10%〜+10%: n=86 hit%=40.7% ROI=1.12 (コスト 19,500/回収 21,780)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料


以下、詳細セクション（通常読み飛ばし可）

## 環境・コード状態
- git_sha: `<error: Command '['git', '-C', '/opt/boa` dirty=True
- config.json md5: `eb532e851a30cd2f7e69bdf0dfca3f2b`
- strategies.json md5: `06b22dd935785e7947bf9c0f170b69a3`
- numpy=2.4.4 lightgbm=4.6.0 scipy=1.17.1
- **calibration_applied**: True ← predictor.py が校正を呼んでるか
- DB: 16.87MB / last modified 2026-10-26T12:49:46.812176+09:00

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
d=20261026: HTTPSConnectionPool(host='www.boatrace.jp', port=443): Read timed out. (read timeout=10), retry in 1s
2026-10-26 12:49:28,315 [INFO] scraper: odds3t: 120/120 parsed
2026-10-26 12:49:29,634 [INFO] scraper: odds3f: 20/20 parsed
2026-10-26 12:49:30,721 [INFO] scraper: odds2t: 30/30 parsed
2026-10-26 12:49:30,722 [INFO] scraper: odds2f: 12/15 parsed
2026-10-26 12:49:31,843 [INFO] scraper: odds_win: 4/6 parsed
2026-10-26 12:49:31,843 [INFO] scraper: fetch_race 09/6: boats=6 odds=186/191
2026-10-26 12:49:31,846 [INFO] predictor: CALIBRATION_MODE=on
2026-10-26 12:49:31,846 [INFO] predictor: combos: {'win': 4, '2t': 30, '3t': 120}
2026-10-26 12:49:31,850 [INFO] run_cycle: fetched 09/6 [final]: 154 combos
2026-10-26 12:49:35,432 [INFO] scraper: odds3t: 120/120 parsed
2026-10-26 12:49:36,542 [INFO] scraper: odds3f: 20/20 parsed
2026-10-26 12:49:37,664 [INFO] scraper: odds2t: 30/30 parsed
2026-10-26 12:49:37,665 [INFO] scraper: odds2f: 15/15 parsed
2026-10-26 12:49:38,778 [INFO] scraper: odds_win: 2/6 parsed
2026-10-26 12:49:38,778 [INFO] scraper: fetch_race 22/5: boats=6 odds=187/191
2026-10-26 12:49:38,780 [INFO] predictor: CALIBRATION_MODE=on
2026-10-26 12:49:38,780 [INFO] predictor: combos: {'win': 2, '2t': 30, '3t': 120}
2026-10-26 12:49:38,784 [INFO] run_cycle: fetched 22/5 [scan]: 152 combos
2026-10-26 12:49:42,671 [INFO] scraper: odds3t: 120/120 parsed
2026-10-26 12:49:43,828 [INFO] scraper: odds3f: 20/20 parsed
2026-10-26 12:49:44,935 [INFO] scraper: odds2t: 30/30 parsed
2026-10-26 12:49:44,936 [INFO] scraper: odds2f: 15/15 parsed
2026-10-26 12:49:46,050 [INFO] scraper: odds_win: 4/6 parsed
2026-10-26 12:49:46,050 [INFO] scraper: fetch_race 21/10: boats=6 odds=189/191
2026-10-26 12:49:46,053 [INFO] predictor: CALIBRATION_MODE=on
2026-10-26 12:49:46,053 [INFO] predictor: combos: {'win': 4, '2t': 30, '3t': 120}
2026-10-26 12:49:46,058 [INFO] run_cycle: fetched 21/10 [scan]: 154 combos
2026-10-26 12:49:46,250 [INFO] run_cycle: run_cycle done: 0 notifications

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
{'final': 25, 'result': 11, 'scan': 24}

## アラート件数 (24h・種類別)
```
  ANOMALY_SCRAPER_FAILURE_BURST: 128
  FINAL_MISSING: 61
  CIRCUIT_BREAKER_TRIP: 45
  CIRCUIT_BREAKER_NO_ACTION: 34
  STRATEGY_CI_FAIL: 17
  ANOMALY_SCAN_FINAL_RATIO: 6
  ANOMALY_BET_VOLUME_DROP: 1
```

## 戦略別 ROI (7日)
| sid | n | hits | cost | payout | PL | ROI |
|---|---|---|---|---|---|---|
| S00 | 42 | 10 | 12,600 | 7,530 | -5,070 | 0.598 |
| S01_NAKAANA1 | 51 | 11 | 10,200 | 4,140 | -6,060 | 0.406 |
| S02_TETSUBAN | 9 | 5 | 1,800 | 1,940 | +140 | 1.078 |

## 直近アラート (24h・新しい順)
```
[12:48:05] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1144}
[12:45:39] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1152}
[12:44:05] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1151}
[12:42:50] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1179}
[12:41:37] CIRCUIT_BREAKER_TRIP: {"cost": 12600, "kind": "CIRCUIT_BREAKER_TRIP", "n": 42, "payout": 7530, "roi_7d": 0.598, "sid": "S00"}
[12:41:37] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1168}
[12:40:35] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1154}
[12:39:27] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1180}
[12:38:28] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1173}
[12:37:28] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1157}
```

## 本日残レース: 90件

## 本日nidレジャー（ID単位完遂突合せ）
- race_schedule: 144件 登録 / 54件 締切済
- 通知発射: scan=7 nid / final=10 nid / result=4 nid
- predictions: 7 / うち結果DB記録済: 5
- ✅ 結果DBあるが通知未発射: 0件 `tools/backfill_result_notifications.py` で救済可
- ✅ scan後final無しのまま締切: 0件（FINAL_MISSING の温床）

## 直近送信失敗 (24h)
```
```

## 最新 predictions サンプル (計算spot-check用)
| sid | race | bt | combo | p | odds | ev | bet | at |
|---|---|---|---|---|---|---|---|---|
| S00 | 045R | win | 1 | 0.4989 | 5.2 | 2.59 | 300 | scan=- drift=- | 12:41:20 |
| S01_NAKAANA1 | 224R | win | 1 | 0.5476 | 4.6 | 2.52 | 200 | scan=- drift=- | 12:29:19 |
| S00 | 085R | win | 1 | 0.5123 | 17.2 | 8.81 | 300 | scan=10.5 drift=+63.8% | 12:11:19 |
| S00 | 094R | win | 1 | 0.1957 | 12.7 | 2.49 | 300 | scan=6.0 drift=+111.7% | 11:53:43 |
| S01_NAKAANA1 | 083R | win | 1 | 0.4111 | 4.5 | 1.85 | 200 | scan=- drift=- | 11:11:26 |
| S00 | 083R | win | 1 | 0.4111 | 4.5 | 1.85 | 300 | scan=- drift=- | 11:11:20 |
| S01_NAKAANA1 | 112R | win | 1 | 0.4111 | 3.5 | 1.44 | 200 | scan=3.5 drift=+0.0% | 10:52:19 |
| S02_TETSUBAN | 208R | win | 1 | 0.6026 | 2.8 | 1.69 | 200 | scan=- drift=- | 21:14:20 |
| S01_NAKAANA1 | 248R | win | 1 | 0.4111 | 3.6 | 1.48 | 200 | scan=- drift=- | 18:23:20 |
| S00 | 0810R | win | 1 | 0.5990 | 6.6 | 3.95 | 300 | scan=29.2 drift=-77.4% | 14:46:18 |

## オッズドリフト統計 (7日)

| bt | n | avg | min | max | down10 | collapse(≤-30%) | any_large(≥10%) |
|---|---|---|---|---|---|---|---|
| win | 50 | +19.1% | -77.4% | +369.8% | 10 | 3 | 31 |

## 校正テーブル合格状況

- total: 27 グループ
- passed: 19
- failed: 8 — `2f|4, 2f|5, 3f|2, 3f|3, 3f|4, 3t|1, 3t|4, 3t|5`
- 主力グループ状態: ✅ (全12グループ合格)

## SRE Golden Signals (24h)

| Signal | Value |
|---|---|
| **Latency** (scan→final avg) | 450.5s |
| **Latency** (scan→final max) | 648.0s |
| **Traffic** (notifications 24h) | 60 |
| **Errors** (send fail rate) | ✅ 0.0% |
| **Saturation** (S00) | 1,200円 used |
| **Saturation** (S01_NAKAANA1) | 600円 used |

## 信ぴょう性メトリクス（予測精度の証拠）

### bt別: 予測確率 vs 実的中率
| bt | n | 予測avg | 実的中率 | 校正誤差 | 過信度 | Brier |
|---|---|---|---|---|---|---|
| win | 446 | 0.4793 | 0.3475 | +0.1318 | 🟡+28% | 0.2385 |

### 戦略別: 校正精度 + Brier Skill Score
| sid | bt | n | pred | actual | Brier | BSS | ROI |
|---|---|---|---|---|---|---|---|
| S00 | win | 185 | 0.4432 | 0.2919 | 0.2334 | 🔴-0.13 | 0.791 |
| S01_NAKAANA1 | win | 190 | 0.4897 | 0.3368 | 0.2373 | 🔴-0.06 | 0.901 |
| S02_TETSUBAN | win | 71 | 0.5456 | 0.5211 | 0.2549 | 🔴-0.02 | 0.9 |

### 確率デシル別: 校正カーブ
| 確率帯 | n | 予測avg | 実的中率 | gap |
|---|---|---|---|---|
| 0.15-0.20 | 9 | 0.1865 | 0.0000 | 🔴+0.1865 |
| 0.20-0.30 | 9 | 0.2288 | 0.2222 | ✅+0.0066 |
| 0.30-0.50 | 153 | 0.4112 | 0.3007 | 🔴+0.1105 |
| 0.50+ | 270 | 0.5430 | 0.3889 | 🔴+0.1541 |

## Settlement Ratio データ品質

- 学習済み: 4バンド / fallback: 13バンド
| bt | odds帯 | source | n | ratio |
|---|---|---|---|---|
| win | <3.0 | ✅learned | 193 | 0.779 |
| win | <5.0 | ✅learned | 351 | 0.741 |
| win | <10.0 | ✅learned | 154 | 0.452 |
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
_auto-generated by claude_snapshot.py at 2026-10-26T12:50:01.722922+09:00_