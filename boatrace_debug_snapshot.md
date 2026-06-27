# ClaudeDebug スナップショット

## 🔴 現状: RED

**生成**: 2026-06-27T18:00:02.401814+09:00

### 次に取るべきアクション
> RED最優先: CALIBRATION_DRIFT×36 (24h) → ログ/DB確認

### 検出された問題
- 🟡 FINAL_MISSING×41 (24h)
- 🔴 CALIBRATION_DRIFT×36 (24h)
- 🔴 CIRCUIT_BREAKER_TRIP×27 (24h)
- 🔴 PSI_DRIFT_DETECTED×22 (24h)
- 🔴 STRATEGY_CI_FAIL×17 (24h)
- 🟡 LARGE_ODDS_DRIFT×1 (24h)
- 🔴 SEND_WITHOUT_DBREC×1 (24h)
- 🔴 alert_manager dispatch 失敗確定 1件（手動確認必要）

---

## 🔧 AI デバッグキュー（このClaudeが対処）

### 🔴 CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION  ×1  [2026-06-27T18:00:04]
- key: `CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION|戦略 S00 が TRIP してるが enabled のまま`
- **FIX**: CIRCUIT_BREAKER_TRIP 戦略が enabled のまま。enabled:false に

### 🔴 CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION  ×1  [2026-06-27T18:00:04]
- key: `CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION|戦略 S01_NAKAANA1 が TRIP してるが enabled のまま`
- **FIX**: CIRCUIT_BREAKER_TRIP 戦略が enabled のまま。enabled:false に

### 🔴 PSI_DRIFT_DETECTED  ×36  [2026-06-27T17:24:21]
- key: `PSI_DRIFT_DETECTED|`
- **FIX**: ml_prob 分布の PSI>0.25→モデル入力の分布シフト。校正テーブル再生成 or モデル再学習を検討

### 🟡 KS_ODDS_DRIFT  ×42  [2026-06-27T17:18:22]
- key: `KS_ODDS_DRIFT|`
- **FIX**: オッズ分布の KS 検定 p<0.01→市場構造変化の可能性。settlement_ratio の fallback 値を再検証

### 🟡 ANOMALY_SCAN_FINAL_RATIO  ×43  [2026-06-27T17:17:08]
- key: `ANOMALY_SCAN_FINAL_RATIO|`
- **FIX**: scan→final成立率が7日baselineから2σ逸脱。scan/final window設定・odds取得タイミング

### 🔴 CALIBRATION_DRIFT  ×57  [2026-06-27T17:03:52]
- key: `CALIBRATION_DRIFT|`
- **FIX**: 予測確率が実的中率から50%以上乖離→isotonic_calibration.json 再生成 or モデル再学習が必要。EV計算が膨張中

### 🔴 CIRCUIT_BREAKER_TRIP  ×57  [2026-06-27T17:03:52]
- key: `CIRCUIT_BREAKER_TRIP|`
- **FIX**: 7日ROI<0.7→戦略を enabled:false にして原因調査。校正ドリフトか市場変化を確認

### 🔴 CIRCUIT_BREAKER_NO_ACTION  ×114  [2026-06-27T17:03:52]
- key: `CIRCUIT_BREAKER_NO_ACTION|`
- **FIX**: CIRCUIT_BREAKER_TRIP 発動済なのに strategies.json で enabled のまま。enabled:false に切替 or 復旧条件満たしたか確認

### 🔴 STRATEGY_CI_FAIL  ×57  [2026-06-27T17:03:52]
- key: `STRATEGY_CI_FAIL|`
- **FIX**: grid戦略のOOS CI下限<1.0→論文基準で赤字リスク。strategies.json確認

### 🟡 ANOMALY_SCRAPER_FAILURE_BURST  ×60  [2026-06-27T17:00:56]
- key: `ANOMALY_SCRAPER_FAILURE_BURST|`
- **FIX**: 直近1h でscraper 3-retry 全敗多発。boatrace.jp 側timeout / IP ban / DDoS

### 🔴 SEND_WITHOUT_DBREC  ×1  [2026-06-27T13:52:25]
- key: `SEND_WITHOUT_DBREC|`
- **FIX**: record_notification の例外→DB書込エラー原因特定（WAL、ロック）

### 🟡 ANOMALY_BET_VOLUME_DROP  ×58  [2026-06-27T12:00:34]
- key: `ANOMALY_BET_VOLUME_DROP|`
- **FIX**: 本日のbet数が7日baselineから2σ低下。戦略filter/ scan fix/run_cycle停止を疑え

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-06-27T06:00:09]
- key: `INSUFFICIENT_SAMPLE|S02_TETSUBAN: n=74<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### 🟡 ORPHAN_SCAN  ×1  [2026-06-27T06:00:09]
- key: `ORPHAN_SCAN|149 件の scan に final/retreat 追従無し`
- **FIX**: scan 後 final も retreat も無い→当該レースの final 窓が短すぎ/fetch 失敗

### ℹ️ DRIFT_BUCKET  ×1  [2026-06-27T06:00:09]
- key: `DRIFT_BUCKET|drift -30%〜-10%: n=36 hit%=22.2% ROI=0.47 (コスト 8,500/回収 4,030)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ CALIBRATION_LIVE  ×1  [2026-06-27T06:00:09]
- key: `CALIBRATION_LIVE|decile 0.20-0.30: n=11 pred=0.2250 actual=0.0000 gap=+0.2250`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-06-27T06:00:09]
- key: `ROI_STAT|S00: n=164 hit%=24.4% hit_CI[Bonf]=[16.1,35.2]% ROI=0.63 ROI_boot95=[0.45,0.83]`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-06-27T06:00:09]
- key: `INSUFFICIENT_SAMPLE|S00: n=164<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ ROI_STAT  ×1  [2026-06-27T06:00:09]
- key: `ROI_STAT|S01_NAKAANA1: n=145 hit%=30.3% hit_CI[Bonf]=[20.6,42.2]% ROI=0.80 ROI_boot95=[0.`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-06-27T06:00:09]
- key: `INSUFFICIENT_SAMPLE|S01_NAKAANA1: n=145<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留


以下、詳細セクション（通常読み飛ばし可）

## 環境・コード状態
- git_sha: `<error: Command '['git', '-C', '/opt/boa` dirty=True
- config.json md5: `eb532e851a30cd2f7e69bdf0dfca3f2b`
- strategies.json md5: `06b22dd935785e7947bf9c0f170b69a3`
- numpy=2.4.4 lightgbm=4.6.0 scipy=1.17.1
- **calibration_applied**: True ← predictor.py が校正を呼んでるか
- DB: 6.24MB / last modified 2026-06-27T18:00:08.536327+09:00

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
d
2026-06-27 17:58:19,996 [INFO] scraper: fetch_race 22/12: boats=6 odds=191/191
2026-06-27 17:58:20,006 [INFO] predictor: CALIBRATION_MODE=on
2026-06-27 17:58:20,006 [INFO] predictor: combos: {'win': 6, '2t': 30, '3t': 120}
2026-06-27 17:58:20,015 [INFO] run_cycle: fetched 22/12 [final]: 156 combos
2026-06-27 17:58:23,529 [INFO] scraper: odds3t: 120/120 parsed
2026-06-27 17:58:24,694 [INFO] scraper: odds3f: 20/20 parsed
2026-06-27 17:58:25,774 [INFO] scraper: odds2t: 30/30 parsed
2026-06-27 17:58:25,775 [INFO] scraper: odds2f: 14/15 parsed
2026-06-27 17:58:26,879 [INFO] scraper: odds_win: 5/6 parsed
2026-06-27 17:58:26,879 [INFO] scraper: fetch_race 07/6: boats=6 odds=189/191
2026-06-27 17:58:26,888 [INFO] predictor: CALIBRATION_MODE=on
2026-06-27 17:58:26,888 [INFO] predictor: combos: {'win': 5, '2t': 30, '3t': 120}
2026-06-27 17:58:26,896 [INFO] run_cycle: fetched 07/6 [scan]: 155 combos
2026-06-27 17:58:26,988 [INFO] run_cycle: run_cycle done: 0 notifications
2026-06-27 17:59:04,107 [INFO] run_cycle: === run_cycle 17:59:04 ===
2026-06-27 17:59:04,107 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-06-27 17:59:04,108 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-06-27 17:59:04,152 [INFO] predictor: Models loaded OK
2026-06-27 17:59:15,695 [INFO] scraper: odds3t: 120/120 parsed
2026-06-27 17:59:16,802 [INFO] scraper: odds3f: 20/20 parsed
2026-06-27 17:59:17,940 [INFO] scraper: odds2t: 30/30 parsed
2026-06-27 17:59:17,941 [INFO] scraper: odds2f: 15/15 parsed
2026-06-27 17:59:19,019 [INFO] scraper: odds_win: 6/6 parsed
2026-06-27 17:59:19,019 [INFO] scraper: fetch_race 01/6: boats=6 odds=191/191
2026-06-27 17:59:19,029 [INFO] predictor: CALIBRATION_MODE=on
2026-06-27 17:59:19,029 [INFO] predictor: combos: {'win': 6, '2t': 30, '3t': 120}
2026-06-27 17:59:19,036 [INFO] run_cycle: fetched 01/6 [final]: 156 combos
2026-06-27 17:59:19,190 [INFO] run_cycle: run_cycle done: 0 notifications

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
    "c": 65
  },
  {
    "target": "primary",
    "ok": 1,
    "c": 65
  }
]
```

## Phase別通知記録 (24h)
{'final': 23, 'result': 12, 'scan': 30}

## アラート件数 (24h・種類別)
```
  ANOMALY_SCRAPER_FAILURE_BURST: 243
  FINAL_MISSING: 41
  CALIBRATION_DRIFT: 36
  CIRCUIT_BREAKER_NO_ACTION: 34
  KS_ODDS_DRIFT: 33
  CIRCUIT_BREAKER_TRIP: 27
  PSI_DRIFT_DETECTED: 22
  ANOMALY_SCAN_FINAL_RATIO: 20
  STRATEGY_CI_FAIL: 17
  ANOMALY_BET_VOLUME_DROP: 2
  LARGE_ODDS_DRIFT: 1
  SEND_WITHOUT_DBREC: 1
```

## 戦略別 ROI (7日)
| sid | n | hits | cost | payout | PL | ROI |
|---|---|---|---|---|---|---|
| S00 | 51 | 10 | 15,300 | 7,170 | -8,130 | 0.469 |
| S01_NAKAANA1 | 30 | 9 | 6,000 | 5,040 | -960 | 0.84 |
| S02_TETSUBAN | 7 | 0 | 1,400 | 0 | -1,400 | 0.0 |

## 直近アラート (24h・新しい順)
```
[17:59:19] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 913}
[17:58:27] FINAL_MISSING: {"deadline": "2026-06-27T16:28:00+09:00", "kind": "FINAL_MISSING", "nid": "2026062724031628", "sid": "S00"}
[17:58:27] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 906}
[17:56:05] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 917}
[17:55:39] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 911}
[17:54:39] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 4, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 909}
[17:51:22] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 4, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 894}
[17:50:45] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 4, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 885}
[17:49:28] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 907}
[17:47:28] FINAL_MISSING: {"deadline": "2026-06-27T13:14:00+09:00", "kind": "FINAL_MISSING", "nid": "2026062702061314", "sid": "S00"}
```

## 本日残レース: 26件

## 本日nidレジャー（ID単位完遂突合せ）
- race_schedule: 180件 登録 / 154件 締切済
- 通知発射: scan=25 nid / final=18 nid / result=9 nid
- predictions: 9 / うち結果DB記録済: 9
- ✅ 結果DBあるが通知未発射: 0件 `tools/backfill_result_notifications.py` で救済可
- 🔴 scan後final無しのまま締切: 10件（FINAL_MISSING の温床）

## 直近送信失敗 (24h)
```
```

## 最新 predictions サンプル (計算spot-check用)
| sid | race | bt | combo | p | odds | ev | bet | at |
|---|---|---|---|---|---|---|---|---|
| S00 | 1710R | win | 1 | 0.5719 | 5.6 | 3.20 | 300 | scan=8.2 drift=-31.7% | 15:24:21 |
| S00 | 038R | win | 1 | 0.4989 | 17.2 | 8.58 | 300 | scan=5.2 drift=+230.8% | 14:21:41 |
| S00 | 178R | win | 1 | 0.4111 | 5.3 | 2.18 | 300 | scan=- drift=- | 14:21:33 |
| S00 | 028R | win | 1 | 0.4111 | 11.5 | 4.73 | 300 | scan=11.0 drift=+4.5% | 14:13:32 |
| S02_TETSUBAN | 2111R | win | 1 | 0.5334 | 2.2 | 1.17 | 200 | scan=2.6 drift=-15.4% | 13:20:36 |
| S01_NAKAANA1 | 026R | win | 1 | 0.5123 | 3.7 | 1.90 | 200 | scan=3.8 drift=-2.6% | 13:11:27 |
| S00 | 176R | win | 1 | 0.3177 | 9.7 | 3.08 | 300 | scan=9.3 drift=+4.3% | 13:08:21 |
| S00 | 022R | win | 1 | 0.5174 | 4.9 | 2.54 | 300 | scan=10.5 drift=-53.3% | 11:13:21 |
| S00 | 031R | win | 1 | 0.5123 | 4.2 | 2.15 | 300 | scan=- drift=- | 11:11:51 |
| S02_TETSUBAN | 079R | win | 1 | 0.5891 | 2.4 | 1.41 | 200 | scan=- drift=- | 19:22:23 |

## オッズドリフト統計 (7日)

| bt | n | avg | min | max | down10 | collapse(≤-30%) | any_large(≥10%) |
|---|---|---|---|---|---|---|---|
| win | 51 | +27.7% | -53.3% | +482.2% | 17 | 7 | 34 |

## 校正テーブル合格状況

- total: 27 グループ
- passed: 19
- failed: 8 — `2f|4, 2f|5, 3f|2, 3f|3, 3f|4, 3t|1, 3t|4, 3t|5`
- 主力グループ状態: ✅ (全12グループ合格)

## SRE Golden Signals (24h)

| Signal | Value |
|---|---|
| **Latency** (scan→final avg) | 477.1s |
| **Latency** (scan→final max) | 654.8s |
| **Traffic** (notifications 24h) | 65 |
| **Errors** (send fail rate) | ✅ 0.0% |
| **Saturation** (S00) | 2,100円 used |
| **Saturation** (S01_NAKAANA1) | 200円 used |
| **Saturation** (S02_TETSUBAN) | 200円 used |

## 信ぴょう性メトリクス（予測精度の証拠）

### bt別: 予測確率 vs 実的中率
| bt | n | 予測avg | 実的中率 | 校正誤差 | 過信度 | Brier |
|---|---|---|---|---|---|---|
| win | 379 | 0.4773 | 0.2744 | +0.2029 | 🟡+42% | 0.2404 |

### 戦略別: 校正精度 + Brier Skill Score
| sid | bt | n | pred | actual | Brier | BSS | ROI |
|---|---|---|---|---|---|---|---|
| S00 | win | 168 | 0.4372 | 0.2500 | 0.2249 | 🔴-0.20 | 0.645 |
| S01_NAKAANA1 | win | 138 | 0.4915 | 0.2971 | 0.2426 | 🔴-0.16 | 0.788 |
| S02_TETSUBAN | win | 73 | 0.5429 | 0.2877 | 0.2718 | 🔴-0.33 | 0.452 |

### 確率デシル別: 校正カーブ
| 確率帯 | n | 予測avg | 実的中率 | gap |
|---|---|---|---|---|
| 0.15-0.20 | 9 | 0.1819 | 0.3333 | 🔴-0.1514 |
| 0.20-0.30 | 11 | 0.2250 | 0.0000 | 🔴+0.2250 |
| 0.30-0.50 | 126 | 0.4227 | 0.2143 | 🔴+0.2084 |
| 0.50+ | 226 | 0.5435 | 0.3230 | 🔴+0.2205 |

## Settlement Ratio データ品質

- 学習済み: 4バンド / fallback: 13バンド
| bt | odds帯 | source | n | ratio |
|---|---|---|---|---|
| win | <3.0 | ✅learned | 46 | 0.733 |
| win | <5.0 | ✅learned | 98 | 0.729 |
| win | <10.0 | ✅learned | 58 | 0.493 |
| win | <20.0 | ✅learned | 17 | 0.211 |
| win | <50.0 | ⚠️fallback | 2 | 0.1 |
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
_auto-generated by claude_snapshot.py at 2026-06-27T18:00:02.401814+09:00_