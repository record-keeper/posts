# ClaudeDebug スナップショット

## 🔴 現状: RED

**生成**: 2026-08-15T12:30:02.117279+09:00

### 次に取るべきアクション
> RED最優先: CIRCUIT_BREAKER_TRIP×50 (24h) → ログ/DB確認

### 検出された問題
- 🟡 FINAL_MISSING×75 (24h)
- 🔴 CIRCUIT_BREAKER_TRIP×50 (24h)
- 🔴 STRATEGY_CI_FAIL×17 (24h)
- 🟡 LARGE_ODDS_DRIFT×1 (24h)
- 🔴 alert_manager dispatch 失敗確定 1件（手動確認必要）

---

## 🔧 AI デバッグキュー（このClaudeが対処）

### 🔴 CIRCUIT_BREAKER_TRIP  ×54  [2026-08-15T12:03:32]
- key: `CIRCUIT_BREAKER_TRIP|`
- **FIX**: 7日ROI<0.7→戦略を enabled:false にして原因調査。校正ドリフトか市場変化を確認

### 🔴 CIRCUIT_BREAKER_NO_ACTION  ×81  [2026-08-15T12:03:32]
- key: `CIRCUIT_BREAKER_NO_ACTION|`
- **FIX**: CIRCUIT_BREAKER_TRIP 発動済なのに strategies.json で enabled のまま。enabled:false に切替 or 復旧条件満たしたか確認

### 🔴 STRATEGY_CI_FAIL  ×27  [2026-08-15T12:03:32]
- key: `STRATEGY_CI_FAIL|`
- **FIX**: grid戦略のOOS CI下限<1.0→論文基準で赤字リスク。strategies.json確認

### 🔴 CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION  ×2  [2026-08-15T12:00:04]
- key: `CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION|戦略 S00 が TRIP してるが enabled のまま`
- **FIX**: CIRCUIT_BREAKER_TRIP 戦略が enabled のまま。enabled:false に

### 🔴 CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION  ×2  [2026-08-15T12:00:04]
- key: `CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION|戦略 S01_NAKAANA1 が TRIP してるが enabled のまま`
- **FIX**: CIRCUIT_BREAKER_TRIP 戦略が enabled のまま。enabled:false に

### 🔴 CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION  ×2  [2026-08-15T12:00:04]
- key: `CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION|戦略 S02_TETSUBAN が TRIP してるが enabled のまま`
- **FIX**: CIRCUIT_BREAKER_TRIP 戦略が enabled のまま。enabled:false に

### 🟡 ANOMALY_SCRAPER_FAILURE_BURST  ×30  [2026-08-15T11:52:02]
- key: `ANOMALY_SCRAPER_FAILURE_BURST|`
- **FIX**: 直近1h でscraper 3-retry 全敗多発。boatrace.jp 側timeout / IP ban / DDoS

### 🟡 ANOMALY_SCAN_FINAL_RATIO  ×14  [2026-08-15T11:40:37]
- key: `ANOMALY_SCAN_FINAL_RATIO|`
- **FIX**: scan→final成立率が7日baselineから2σ逸脱。scan/final window設定・odds取得タイミング

### 🟡 ANOMALY_BET_VOLUME_DROP  ×38  [2026-08-15T11:00:30]
- key: `ANOMALY_BET_VOLUME_DROP|`
- **FIX**: 本日のbet数が7日baselineから2σ低下。戦略filter/ scan fix/run_cycle停止を疑え

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-08-15T06:00:09]
- key: `INSUFFICIENT_SAMPLE|S02_TETSUBAN: n=72<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-08-15T06:00:09]
- key: `INSUFFICIENT_SAMPLE|S00: n=174<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ ROI_STAT  ×1  [2026-08-15T06:00:09]
- key: `ROI_STAT|S00: n=174 hit%=21.8% hit_CI[Bonf]=[14.2,32.1]% ROI=0.62 ROI_boot95=[0.42,0.84]`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-08-15T06:00:09]
- key: `ROI_STAT|S01_NAKAANA1: n=168 hit%=20.2% hit_CI[Bonf]=[12.8,30.5]% ROI=0.64 ROI_boot95=[0.`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-08-15T06:00:09]
- key: `INSUFFICIENT_SAMPLE|S01_NAKAANA1: n=168<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ ROI_STAT  ×1  [2026-08-15T06:00:09]
- key: `ROI_STAT|S02_TETSUBAN: n=72 hit%=54.2% hit_CI[Bonf]=[37.7,69.8]% ROI=0.90 ROI_boot95=[0.6`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### 🟡 ORPHAN_SCAN  ×1  [2026-08-15T06:00:09]
- key: `ORPHAN_SCAN|194 件の scan に final/retreat 追従無し`
- **FIX**: scan 後 final も retreat も無い→当該レースの final 窓が短すぎ/fetch 失敗

### ℹ️ DRIFT_BUCKET  ×1  [2026-08-15T06:00:09]
- key: `DRIFT_BUCKET|drift ≤-30%: n=39 hit%=20.5% ROI=0.60 (コスト 11,200/回収 6,770)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-08-15T06:00:09]
- key: `DRIFT_BUCKET|drift -30%〜-10%: n=35 hit%=34.3% ROI=0.99 (コスト 8,500/回収 8,450)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-08-15T06:00:09]
- key: `DRIFT_BUCKET|drift -10%〜+10%: n=70 hit%=25.7% ROI=0.58 (コスト 16,500/回収 9,650)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-08-15T06:00:09]
- key: `DRIFT_BUCKET|drift +10%〜+30%: n=48 hit%=25.0% ROI=0.51 (コスト 11,100/回収 5,620)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料


以下、詳細セクション（通常読み飛ばし可）

## 環境・コード状態
- git_sha: `<error: Command '['git', '-C', '/opt/boa` dirty=True
- config.json md5: `eb532e851a30cd2f7e69bdf0dfca3f2b`
- strategies.json md5: `06b22dd935785e7947bf9c0f170b69a3`
- numpy=2.4.4 lightgbm=4.6.0 scipy=1.17.1
- **calibration_applied**: True ← predictor.py が校正を呼んでるか
- DB: 10.58MB / last modified 2026-08-15T12:29:38.175464+09:00

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
2026-08-15 12:29:18,740 [INFO] scraper: odds2f: 15/15 parsed
2026-08-15 12:29:19,809 [INFO] scraper: odds_win: 5/6 parsed
2026-08-15 12:29:19,809 [INFO] scraper: fetch_race 05/3: boats=6 odds=189/191
2026-08-15 12:29:19,813 [INFO] predictor: CALIBRATION_MODE=on
2026-08-15 12:29:19,813 [INFO] predictor: combos: {'win': 5, '2t': 29, '3t': 120}
2026-08-15 12:29:19,816 [INFO] run_cycle: fetched 05/3 [final]: 154 combos
2026-08-15 12:29:20,398 [INFO] race_id: notif: nid=2026081505031231 sid=S00 phase=final rank=SS
2026-08-15 12:29:20,759 [INFO] notifier: Discord notify OK (status=204)
2026-08-15 12:29:21,380 [INFO] notifier: Discord notify OK (status=204)
2026-08-15 12:29:21,559 [INFO] run_cycle: FINAL S00 多摩川3R SS
2026-08-15 12:29:25,318 [INFO] scraper: odds3t: 120/120 parsed
2026-08-15 12:29:26,415 [INFO] scraper: odds3f: 20/20 parsed
2026-08-15 12:29:27,501 [INFO] scraper: odds2t: 29/30 parsed
2026-08-15 12:29:27,503 [INFO] scraper: odds2f: 14/15 parsed
2026-08-15 12:29:28,566 [INFO] scraper: odds_win: 4/6 parsed
2026-08-15 12:29:28,566 [INFO] scraper: fetch_race 08/5: boats=6 odds=187/191
2026-08-15 12:29:28,569 [INFO] predictor: CALIBRATION_MODE=on
2026-08-15 12:29:28,569 [INFO] predictor: combos: {'win': 4, '2t': 29, '3t': 120}
2026-08-15 12:29:28,573 [INFO] run_cycle: fetched 08/5 [scan]: 153 combos
2026-08-15 12:29:32,054 [INFO] scraper: odds3t: 120/120 parsed
2026-08-15 12:29:33,159 [INFO] scraper: odds3f: 20/20 parsed
2026-08-15 12:29:34,263 [INFO] scraper: odds2t: 29/30 parsed
2026-08-15 12:29:34,264 [INFO] scraper: odds2f: 14/15 parsed
2026-08-15 12:29:35,325 [INFO] scraper: odds_win: 4/6 parsed
2026-08-15 12:29:35,325 [INFO] scraper: fetch_race 18/9: boats=6 odds=187/191
2026-08-15 12:29:35,328 [INFO] predictor: CALIBRATION_MODE=on
2026-08-15 12:29:35,328 [INFO] predictor: combos: {'win': 4, '2t': 29, '3t': 120}
2026-08-15 12:29:35,332 [INFO] run_cycle: fetched 18/9 [scan]: 153 combos
2026-08-15 12:29:35,435 [INFO] run_cycle: run_cycle done: 1 notifications

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
    "c": 88
  },
  {
    "target": "primary",
    "ok": 1,
    "c": 88
  }
]
```

## Phase別通知記録 (24h)
{'final': 34, 'result': 13, 'scan': 41}

## アラート件数 (24h・種類別)
```
  ANOMALY_SCRAPER_FAILURE_BURST: 240
  FINAL_MISSING: 75
  CIRCUIT_BREAKER_NO_ACTION: 50
  CIRCUIT_BREAKER_TRIP: 50
  STRATEGY_CI_FAIL: 17
  ANOMALY_SCAN_FINAL_RATIO: 7
  ANOMALY_BET_VOLUME_DROP: 2
  LARGE_ODDS_DRIFT: 1
```

## 戦略別 ROI (7日)
| sid | n | hits | cost | payout | PL | ROI |
|---|---|---|---|---|---|---|
| S00 | 47 | 11 | 14,100 | 9,330 | -4,770 | 0.662 |
| S01_NAKAANA1 | 47 | 7 | 9,400 | 4,620 | -4,780 | 0.491 |
| S02_TETSUBAN | 22 | 12 | 4,400 | 3,260 | -1,140 | 0.741 |

## 直近アラート (24h・新しい順)
```
[12:29:35] CIRCUIT_BREAKER_TRIP: {"cost": 14100, "kind": "CIRCUIT_BREAKER_TRIP", "n": 47, "payout": 9330, "roi_7d": 0.662, "sid": "S00"}
[12:29:35] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1470}
[12:28:37] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1450}
[12:27:28] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1462}
[12:27:28] ANOMALY_SCAN_FINAL_RATIO: {"abs_drop": 0.299, "baseline_mean": 0.754, "baseline_stdev": 0.103, "kind": "ANOMALY_SCAN_FINAL_RATIO", "today_ratio": 0.455, "today_scan_count": 11, "z_score": -2.9}
[12:26:38] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1469}
[12:26:38] ANOMALY_SCAN_FINAL_RATIO: {"abs_drop": 0.254, "baseline_mean": 0.754, "baseline_stdev": 0.103, "kind": "ANOMALY_SCAN_FINAL_RATIO", "today_ratio": 0.5, "today_scan_count": 10, "z_score": -2.46}
[12:25:26] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1464}
[12:24:40] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1446}
[12:23:39] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1429}
```

## 本日残レース: 159件

## 本日nidレジャー（ID単位完遂突合せ）
- race_schedule: 216件 登録 / 57件 締切済
- 通知発射: scan=11 nid / final=7 nid / result=2 nid
- predictions: 3 / うち結果DB記録済: 2
- ✅ 結果DBあるが通知未発射: 0件 `tools/backfill_result_notifications.py` で救済可
- 🔴 scan後final無しのまま締切: 3件（FINAL_MISSING の温床）

## 直近送信失敗 (24h)
```
```

## 最新 predictions サンプル (計算spot-check用)
| sid | race | bt | combo | p | odds | ev | bet | at |
|---|---|---|---|---|---|---|---|---|
| S00 | 053R | win | 1 | 0.4111 | 9.0 | 3.70 | 300 | scan=- drift=- | 12:29:19 |
| S01_NAKAANA1 | 108R | win | 1 | 0.5476 | 3.7 | 2.03 | 200 | scan=4.9 drift=-24.5% | 11:47:31 |
| S01_NAKAANA1 | 083R | win | 1 | 0.5476 | 4.9 | 2.68 | 200 | scan=- drift=- | 11:39:36 |
| S00 | 245R | win | 1 | 0.1760 | 5.9 | 1.04 | 300 | scan=5.8 drift=+1.7% | 17:16:18 |
| S02_TETSUBAN | 1310R | win | 1 | 0.5123 | 2.2 | 1.13 | 200 | scan=- drift=- | 15:07:20 |
| S01_NAKAANA1 | 225R | win | 1 | 0.5082 | 3.2 | 1.63 | 200 | scan=4.9 drift=-34.7% | 14:11:30 |
| S00 | 176R | win | 1 | 0.5123 | 45.3 | 23.21 | 300 | scan=41.2 drift=+10.0% | 13:30:20 |
| S01_NAKAANA1 | 036R | win | 1 | 0.5123 | 3.5 | 1.79 | 200 | scan=- drift=- | 13:27:29 |
| S00 | 036R | win | 1 | 0.5123 | 9.0 | 4.61 | 300 | scan=7.3 drift=+23.3% | 13:26:18 |
| S00 | 044R | win | 1 | 0.3177 | 12.3 | 3.91 | 300 | scan=4.0 drift=+207.5% | 13:21:44 |

## オッズドリフト統計 (7日)

| bt | n | avg | min | max | down10 | collapse(≤-30%) | any_large(≥10%) |
|---|---|---|---|---|---|---|---|
| win | 70 | +8.8% | -62.9% | +287.7% | 21 | 9 | 44 |

## 校正テーブル合格状況

- total: 27 グループ
- passed: 19
- failed: 8 — `2f|4, 2f|5, 3f|2, 3f|3, 3f|4, 3t|1, 3t|4, 3t|5`
- 主力グループ状態: ✅ (全12グループ合格)

## SRE Golden Signals (24h)

| Signal | Value |
|---|---|
| **Latency** (scan→final avg) | 477.6s |
| **Latency** (scan→final max) | 611.9s |
| **Traffic** (notifications 24h) | 88 |
| **Errors** (send fail rate) | ✅ 0.0% |
| **Saturation** (S00) | 300円 used |
| **Saturation** (S01_NAKAANA1) | 400円 used |

## 信ぴょう性メトリクス（予測精度の証拠）

### bt別: 予測確率 vs 実的中率
| bt | n | 予測avg | 実的中率 | 校正誤差 | 過信度 | Brier |
|---|---|---|---|---|---|---|
| win | 409 | 0.4654 | 0.2665 | +0.1989 | 🟡+43% | 0.2351 |

### 戦略別: 校正精度 + Brier Skill Score
| sid | bt | n | pred | actual | Brier | BSS | ROI |
|---|---|---|---|---|---|---|---|
| S00 | win | 172 | 0.4158 | 0.2209 | 0.2202 | 🔴-0.28 | 0.623 |
| S01_NAKAANA1 | win | 166 | 0.4903 | 0.1988 | 0.2482 | 🔴-0.56 | 0.639 |
| S02_TETSUBAN | win | 71 | 0.5270 | 0.5352 | 0.2406 | ✅+0.03 | 0.877 |

### 確率デシル別: 校正カーブ
| 確率帯 | n | 予測avg | 実的中率 | gap |
|---|---|---|---|---|
| 0.10-0.15 | 9 | 0.1189 | 0.1111 | ✅+0.0078 |
| 0.15-0.20 | 12 | 0.1827 | 0.0833 | 🔴+0.0994 |
| 0.20-0.30 | 9 | 0.2228 | 0.4444 | 🔴-0.2216 |
| 0.30-0.50 | 156 | 0.4177 | 0.2115 | 🔴+0.2061 |
| 0.50+ | 221 | 0.5418 | 0.3167 | 🔴+0.2251 |

## Settlement Ratio データ品質

- 学習済み: 4バンド / fallback: 13バンド
| bt | odds帯 | source | n | ratio |
|---|---|---|---|---|
| win | <3.0 | ✅learned | 109 | 0.768 |
| win | <5.0 | ✅learned | 183 | 0.733 |
| win | <10.0 | ✅learned | 94 | 0.45 |
| win | <20.0 | ✅learned | 30 | 0.227 |
| win | <50.0 | ⚠️fallback | 7 | 0.1 |
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
_auto-generated by claude_snapshot.py at 2026-08-15T12:30:02.117279+09:00_