# ClaudeDebug スナップショット

## 🔴 現状: RED

**生成**: 2026-10-23T13:30:00.974945+09:00

### 次に取るべきアクション
> RED最優先: CIRCUIT_BREAKER_TRIP×46 (24h) → ログ/DB確認

### 検出された問題
- 🟡 FINAL_MISSING×70 (24h)
- 🔴 CIRCUIT_BREAKER_TRIP×46 (24h)
- 🔴 STRATEGY_CI_FAIL×17 (24h)
- 🔴 SEND_WITHOUT_DBREC×1 (24h)
- 🔴 alert_manager dispatch 失敗確定 1件（手動確認必要）

---

## 🔧 AI デバッグキュー（このClaudeが対処）

### 🟡 ANOMALY_SCRAPER_FAILURE_BURST  ×25  [2026-10-23T13:05:56]
- key: `ANOMALY_SCRAPER_FAILURE_BURST|`
- **FIX**: 直近1h でscraper 3-retry 全敗多発。boatrace.jp 側timeout / IP ban / DDoS

### 🔴 CIRCUIT_BREAKER_TRIP  ×52  [2026-10-23T13:04:28]
- key: `CIRCUIT_BREAKER_TRIP|`
- **FIX**: 7日ROI<0.7→戦略を enabled:false にして原因調査。校正ドリフトか市場変化を確認

### 🔴 CIRCUIT_BREAKER_NO_ACTION  ×52  [2026-10-23T13:04:28]
- key: `CIRCUIT_BREAKER_NO_ACTION|`
- **FIX**: CIRCUIT_BREAKER_TRIP 発動済なのに strategies.json で enabled のまま。enabled:false に切替 or 復旧条件満たしたか確認

### 🔴 STRATEGY_CI_FAIL  ×26  [2026-10-23T13:04:28]
- key: `STRATEGY_CI_FAIL|`
- **FIX**: grid戦略のOOS CI下限<1.0→論文基準で赤字リスク。strategies.json確認

### 🟡 ANOMALY_SCAN_FINAL_RATIO  ×29  [2026-10-23T12:30:47]
- key: `ANOMALY_SCAN_FINAL_RATIO|`
- **FIX**: scan→final成立率が7日baselineから2σ逸脱。scan/final window設定・odds取得タイミング

### 🔴 CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION  ×3  [2026-10-23T12:30:03]
- key: `CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION|戦略 S00 が TRIP してるが enabled のまま`
- **FIX**: CIRCUIT_BREAKER_TRIP 戦略が enabled のまま。enabled:false に

### 🔴 CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION  ×3  [2026-10-23T12:30:03]
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
- DB: 16.52MB / last modified 2026-10-23T13:30:03.146212+09:00

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
sed
2026-10-23 13:29:18,564 [INFO] scraper: odds2f: 15/15 parsed
2026-10-23 13:29:19,659 [INFO] scraper: odds_win: 6/6 parsed
2026-10-23 13:29:19,659 [INFO] scraper: fetch_race 06/7: boats=6 odds=191/191
2026-10-23 13:29:19,662 [INFO] predictor: CALIBRATION_MODE=on
2026-10-23 13:29:19,662 [INFO] predictor: combos: {'win': 6, '2t': 30, '3t': 120}
2026-10-23 13:29:19,666 [INFO] run_cycle: fetched 06/7 [final]: 156 combos
2026-10-23 13:29:23,176 [INFO] scraper: odds3t: 120/120 parsed
2026-10-23 13:29:24,266 [INFO] scraper: odds3f: 18/20 parsed
2026-10-23 13:29:25,377 [INFO] scraper: odds2t: 26/30 parsed
2026-10-23 13:29:25,378 [INFO] scraper: odds2f: 14/15 parsed
2026-10-23 13:29:26,483 [INFO] scraper: odds_win: 2/6 parsed
2026-10-23 13:29:26,483 [INFO] scraper: fetch_race 17/8: boats=6 odds=180/191
2026-10-23 13:29:26,485 [INFO] predictor: CALIBRATION_MODE=on
2026-10-23 13:29:26,485 [INFO] predictor: combos: {'win': 2, '2t': 26, '3t': 120}
2026-10-23 13:29:26,489 [INFO] run_cycle: fetched 17/8 [scan]: 148 combos
2026-10-23 13:29:30,096 [INFO] scraper: odds3t: 120/120 parsed
2026-10-23 13:29:31,187 [INFO] scraper: odds3f: 17/20 parsed
2026-10-23 13:29:32,510 [INFO] scraper: odds2t: 25/30 parsed
2026-10-23 13:29:32,512 [INFO] scraper: odds2f: 11/15 parsed
2026-10-23 13:29:33,693 [INFO] scraper: odds_win: 3/6 parsed
2026-10-23 13:29:33,693 [INFO] scraper: fetch_race 11/8: boats=6 odds=176/191
2026-10-23 13:29:33,696 [INFO] predictor: CALIBRATION_MODE=on
2026-10-23 13:29:33,696 [INFO] predictor: combos: {'win': 3, '2t': 25, '3t': 120}
2026-10-23 13:29:33,699 [INFO] run_cycle: fetched 11/8 [scan]: 148 combos
2026-10-23 13:29:33,842 [INFO] race_id: notif: nid=2026102311081342 sid=S00 phase=scan rank=S
2026-10-23 13:29:34,208 [INFO] notifier: Discord notify OK (status=204)
2026-10-23 13:29:34,712 [INFO] notifier: Discord notify OK (status=204)
2026-10-23 13:29:34,717 [INFO] run_cycle: SCAN S00 びわこ8R S
2026-10-23 13:29:34,837 [INFO] run_cycle: run_cycle done: 1 notifications

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
    "c": 61
  },
  {
    "target": "primary",
    "ok": 1,
    "c": 61
  }
]
```

## Phase別通知記録 (24h)
{'final': 24, 'result': 13, 'scan': 24}

## アラート件数 (24h・種類別)
```
  ANOMALY_SCRAPER_FAILURE_BURST: 70
  FINAL_MISSING: 70
  CIRCUIT_BREAKER_TRIP: 46
  CIRCUIT_BREAKER_NO_ACTION: 33
  STRATEGY_CI_FAIL: 17
  ANOMALY_SCAN_FINAL_RATIO: 11
  SEND_WITHOUT_DBREC: 1
```

## 戦略別 ROI (7日)
| sid | n | hits | cost | payout | PL | ROI |
|---|---|---|---|---|---|---|
| S00 | 31 | 7 | 9,300 | 5,790 | -3,510 | 0.623 |
| S01_NAKAANA1 | 48 | 12 | 9,600 | 5,640 | -3,960 | 0.588 |
| S02_TETSUBAN | 15 | 8 | 3,000 | 3,580 | +580 | 1.193 |

## 直近アラート (24h・新しい順)
```
[13:29:34] ANOMALY_SCAN_FINAL_RATIO: {"abs_drop": 0.178, "baseline_mean": 0.845, "baseline_stdev": 0.06, "kind": "ANOMALY_SCAN_FINAL_RATIO", "today_ratio": 0.667, "today_scan_count": 12, "z_score": -2.96}
[13:28:03] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1284}
[13:27:36] CIRCUIT_BREAKER_TRIP: {"cost": 9600, "kind": "CIRCUIT_BREAKER_TRIP", "n": 48, "payout": 5640, "roi_7d": 0.588, "sid": "S01_NAKAANA1"}
[13:27:36] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1280}
[13:26:25] FINAL_MISSING: {"deadline": "2026-10-23T11:55:00+09:00", "kind": "FINAL_MISSING", "nid": "2026102314081155", "sid": "S00"}
[13:26:25] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1271}
[13:25:26] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1269}
[13:24:19] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1275}
[13:23:18] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1290}
[13:21:26] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1297}
```

## 本日残レース: 86件

## 本日nidレジャー（ID単位完遂突合せ）
- race_schedule: 168件 登録 / 82件 締切済
- 通知発射: scan=12 nid / final=13 nid / result=4 nid
- predictions: 6 / うち結果DB記録済: 4
- ✅ 結果DBあるが通知未発射: 0件 `tools/backfill_result_notifications.py` で救済可
- 🔴 scan後final無しのまま締切: 4件（FINAL_MISSING の温床）

## 直近送信失敗 (24h)
```
```

## 最新 predictions サンプル (計算spot-check用)
| sid | race | bt | combo | p | odds | ev | bet | at |
|---|---|---|---|---|---|---|---|---|
| S02_TETSUBAN | 137R | win | 1 | 0.5476 | 2.5 | 1.37 | 200 | scan=- drift=- | 13:19:19 |
| S01_NAKAANA1 | 117R | win | 1 | 0.4111 | 3.6 | 1.48 | 200 | scan=- drift=- | 13:13:18 |
| S01_NAKAANA1 | 066R | win | 1 | 0.5174 | 3.6 | 1.86 | 200 | scan=- drift=- | 12:55:29 |
| S01_NAKAANA1 | 149R | win | 1 | 0.5476 | 3.1 | 1.70 | 200 | scan=3.0 drift=+3.3% | 12:24:18 |
| S00 | 043R | win | 1 | 0.4111 | 10.2 | 4.19 | 300 | scan=- drift=- | 11:45:41 |
| S01_NAKAANA1 | 173R | win | 1 | 0.4989 | 3.7 | 1.85 | 200 | scan=- drift=- | 11:13:19 |
| S00 | 246R | win | 1 | 0.3177 | 4.0 | 1.27 | 300 | scan=4.2 drift=-4.8% | 17:47:18 |
| S01_NAKAANA1 | 126R | win | 1 | 0.5123 | 4.2 | 2.15 | 200 | scan=3.5 drift=+20.0% | 17:26:18 |
| S01_NAKAANA1 | 122R | win | 1 | 0.4111 | 4.2 | 1.73 | 200 | scan=4.2 drift=+0.0% | 15:37:19 |
| S00 | 1110R | win | 1 | 0.5174 | 8.2 | 4.24 | 300 | scan=4.5 drift=+82.2% | 14:27:27 |

## オッズドリフト統計 (7日)

| bt | n | avg | min | max | down10 | collapse(≤-30%) | any_large(≥10%) |
|---|---|---|---|---|---|---|---|
| win | 55 | +29.8% | -52.3% | +495.8% | 7 | 1 | 32 |

## 校正テーブル合格状況

- total: 27 グループ
- passed: 19
- failed: 8 — `2f|4, 2f|5, 3f|2, 3f|3, 3f|4, 3t|1, 3t|4, 3t|5`
- 主力グループ状態: ✅ (全12グループ合格)

## SRE Golden Signals (24h)

| Signal | Value |
|---|---|
| **Latency** (scan→final avg) | 484.4s |
| **Latency** (scan→final max) | 611.8s |
| **Traffic** (notifications 24h) | 61 |
| **Errors** (send fail rate) | ✅ 0.0% |
| **Saturation** (S00) | 300円 used |
| **Saturation** (S01_NAKAANA1) | 800円 used |
| **Saturation** (S02_TETSUBAN) | 200円 used |

## 信ぴょう性メトリクス（予測精度の証拠）

### bt別: 予測確率 vs 実的中率
| bt | n | 予測avg | 実的中率 | 校正誤差 | 過信度 | Brier |
|---|---|---|---|---|---|---|
| win | 445 | 0.4799 | 0.3551 | +0.1248 | 🟡+26% | 0.2434 |

### 戦略別: 校正精度 + Brier Skill Score
| sid | bt | n | pred | actual | Brier | BSS | ROI |
|---|---|---|---|---|---|---|---|
| S00 | win | 179 | 0.4394 | 0.2905 | 0.2369 | 🔴-0.15 | 0.797 |
| S01_NAKAANA1 | win | 185 | 0.4932 | 0.3459 | 0.2431 | 🔴-0.07 | 0.939 |
| S02_TETSUBAN | win | 81 | 0.5391 | 0.5185 | 0.2583 | 🔴-0.03 | 0.953 |

### 確率デシル別: 校正カーブ
| 確率帯 | n | 予測avg | 実的中率 | gap |
|---|---|---|---|---|
| 0.10-0.15 | 6 | 0.1269 | 0.3333 | 🔴-0.2064 |
| 0.15-0.20 | 8 | 0.1824 | 0.0000 | 🔴+0.1824 |
| 0.20-0.30 | 8 | 0.2288 | 0.2500 | ✅-0.0212 |
| 0.30-0.50 | 154 | 0.4147 | 0.3247 | 🔴+0.0900 |
| 0.50+ | 268 | 0.5431 | 0.3843 | 🔴+0.1588 |

## Settlement Ratio データ品質

- 学習済み: 4バンド / fallback: 13バンド
| bt | odds帯 | source | n | ratio |
|---|---|---|---|---|
| win | <3.0 | ✅learned | 191 | 0.782 |
| win | <5.0 | ✅learned | 344 | 0.746 |
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
_auto-generated by claude_snapshot.py at 2026-10-23T13:30:00.974945+09:00_