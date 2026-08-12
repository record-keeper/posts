# ClaudeDebug スナップショット

## 🔴 現状: RED

**生成**: 2026-08-12T13:20:01.968176+09:00

### 次に取るべきアクション
> RED最優先: CIRCUIT_BREAKER_TRIP×22 (24h) → ログ/DB確認

### 検出された問題
- 🟡 FINAL_MISSING×41 (24h)
- 🔴 CIRCUIT_BREAKER_TRIP×22 (24h)
- 🔴 STRATEGY_CI_FAIL×17 (24h)
- 🔴 alert_manager dispatch 失敗確定 1件（手動確認必要）

---

## 🔧 AI デバッグキュー（このClaudeが対処）

### 🟡 ANOMALY_SCAN_FINAL_RATIO  ×15  [2026-08-12T13:05:29]
- key: `ANOMALY_SCAN_FINAL_RATIO|`
- **FIX**: scan→final成立率が7日baselineから2σ逸脱。scan/final window設定・odds取得タイミング

### 🔴 CIRCUIT_BREAKER_TRIP  ×18  [2026-08-12T13:02:23]
- key: `CIRCUIT_BREAKER_TRIP|`
- **FIX**: 7日ROI<0.7→戦略を enabled:false にして原因調査。校正ドリフトか市場変化を確認

### 🔴 CIRCUIT_BREAKER_NO_ACTION  ×18  [2026-08-12T13:02:23]
- key: `CIRCUIT_BREAKER_NO_ACTION|`
- **FIX**: CIRCUIT_BREAKER_TRIP 発動済なのに strategies.json で enabled のまま。enabled:false に切替 or 復旧条件満たしたか確認

### 🔴 STRATEGY_CI_FAIL  ×18  [2026-08-12T13:02:23]
- key: `STRATEGY_CI_FAIL|`
- **FIX**: grid戦略のOOS CI下限<1.0→論文基準で赤字リスク。strategies.json確認

### 🔴 CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION  ×1  [2026-08-12T13:00:05]
- key: `CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION|戦略 S01_NAKAANA1 が TRIP してるが enabled のまま`
- **FIX**: CIRCUIT_BREAKER_TRIP 戦略が enabled のまま。enabled:false に

### 🟡 ANOMALY_SCRAPER_FAILURE_BURST  ×20  [2026-08-12T12:58:06]
- key: `ANOMALY_SCRAPER_FAILURE_BURST|`
- **FIX**: 直近1h でscraper 3-retry 全敗多発。boatrace.jp 側timeout / IP ban / DDoS

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-08-12T06:00:16]
- key: `INSUFFICIENT_SAMPLE|S02_TETSUBAN: n=69<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### 🟡 ORPHAN_SCAN  ×1  [2026-08-12T06:00:16]
- key: `ORPHAN_SCAN|170 件の scan に final/retreat 追従無し`
- **FIX**: scan 後 final も retreat も無い→当該レースの final 窓が短すぎ/fetch 失敗

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-08-12T06:00:16]
- key: `INSUFFICIENT_SAMPLE|S01_NAKAANA1: n=167<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ CALIBRATION_LIVE  ×1  [2026-08-12T06:00:16]
- key: `CALIBRATION_LIVE|decile 0.10-0.15: n=11 pred=0.1216 actual=0.1818 gap=-0.0602`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-08-12T06:00:16]
- key: `ROI_STAT|S00: n=162 hit%=22.2% hit_CI[Bonf]=[14.3,32.9]% ROI=0.63 ROI_boot95=[0.42,0.87]`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-08-12T06:00:16]
- key: `INSUFFICIENT_SAMPLE|S00: n=162<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ ROI_STAT  ×1  [2026-08-12T06:00:16]
- key: `ROI_STAT|S01_NAKAANA1: n=167 hit%=22.2% hit_CI[Bonf]=[14.3,32.6]% ROI=0.68 ROI_boot95=[0.`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-08-12T06:00:16]
- key: `ROI_STAT|S02_TETSUBAN: n=69 hit%=52.2% hit_CI[Bonf]=[35.5,68.3]% ROI=0.89 ROI_boot95=[0.6`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ DRIFT_BUCKET  ×1  [2026-08-12T06:00:16]
- key: `DRIFT_BUCKET|drift ≤-30%: n=37 hit%=21.6% ROI=0.64 (コスト 10,600/回収 6,770)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-08-12T06:00:16]
- key: `DRIFT_BUCKET|drift -30%〜-10%: n=34 hit%=32.4% ROI=0.82 (コスト 8,300/回収 6,810)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-08-12T06:00:16]
- key: `DRIFT_BUCKET|drift -10%〜+10%: n=68 hit%=26.5% ROI=0.57 (コスト 15,800/回収 8,990)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-08-12T06:00:16]
- key: `DRIFT_BUCKET|drift +10%〜+30%: n=47 hit%=23.4% ROI=0.49 (コスト 10,900/回収 5,340)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-08-12T06:00:16]
- key: `DRIFT_BUCKET|drift ≥+30%: n=36 hit%=25.0% ROI=0.97 (コスト 9,900/回収 9,620)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ CALIBRATION_LIVE  ×1  [2026-08-12T06:00:16]
- key: `CALIBRATION_LIVE|bt=win: n=398 pred=0.4672 actual=0.2739 error=+0.1933 (+41%) brier=0.2365 [OVERC`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用


以下、詳細セクション（通常読み飛ばし可）

## 環境・コード状態
- git_sha: `<error: Command '['git', '-C', '/opt/boa` dirty=True
- config.json md5: `eb532e851a30cd2f7e69bdf0dfca3f2b`
- strategies.json md5: `06b22dd935785e7947bf9c0f170b69a3`
- numpy=2.4.4 lightgbm=4.6.0 scipy=1.17.1
- **calibration_applied**: True ← predictor.py が校正を呼んでるか
- DB: 10.17MB / last modified 2026-08-12T13:19:42.298955+09:00

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
rsed
2026-08-12 13:19:24,556 [INFO] scraper: odds2f: 15/15 parsed
2026-08-12 13:19:25,662 [INFO] scraper: odds_win: 4/6 parsed
2026-08-12 13:19:25,662 [INFO] scraper: fetch_race 13/7: boats=6 odds=189/191
2026-08-12 13:19:25,665 [INFO] predictor: CALIBRATION_MODE=on
2026-08-12 13:19:25,665 [INFO] predictor: combos: {'win': 4, '2t': 30, '3t': 120}
2026-08-12 13:19:25,669 [INFO] run_cycle: fetched 13/7 [scan]: 154 combos
2026-08-12 13:19:29,243 [INFO] scraper: odds3t: 120/120 parsed
2026-08-12 13:19:30,313 [INFO] scraper: odds3f: 20/20 parsed
2026-08-12 13:19:31,424 [INFO] scraper: odds2t: 30/30 parsed
2026-08-12 13:19:31,426 [INFO] scraper: odds2f: 15/15 parsed
2026-08-12 13:19:32,533 [INFO] scraper: odds_win: 3/6 parsed
2026-08-12 13:19:32,533 [INFO] scraper: fetch_race 03/6: boats=6 odds=188/191
2026-08-12 13:19:32,535 [INFO] predictor: CALIBRATION_MODE=on
2026-08-12 13:19:32,535 [INFO] predictor: combos: {'win': 3, '2t': 30, '3t': 120}
2026-08-12 13:19:32,539 [INFO] run_cycle: fetched 03/6 [scan]: 153 combos
2026-08-12 13:19:36,198 [INFO] scraper: odds3t: 120/120 parsed
2026-08-12 13:19:37,309 [INFO] scraper: odds3f: 20/20 parsed
2026-08-12 13:19:38,418 [INFO] scraper: odds2t: 30/30 parsed
2026-08-12 13:19:38,419 [INFO] scraper: odds2f: 14/15 parsed
2026-08-12 13:19:39,483 [INFO] scraper: odds_win: 5/6 parsed
2026-08-12 13:19:39,483 [INFO] scraper: fetch_race 06/5: boats=6 odds=189/191
2026-08-12 13:19:39,486 [INFO] predictor: CALIBRATION_MODE=on
2026-08-12 13:19:39,486 [INFO] predictor: combos: {'win': 5, '2t': 30, '3t': 120}
2026-08-12 13:19:39,490 [INFO] run_cycle: fetched 06/5 [scan]: 155 combos
2026-08-12 13:19:39,643 [INFO] race_id: notif: nid=2026081206051332 sid=S00 phase=scan rank=S
2026-08-12 13:19:39,982 [INFO] notifier: Discord notify OK (status=204)
2026-08-12 13:19:42,026 [INFO] notifier: Discord notify OK (status=204)
2026-08-12 13:19:42,144 [INFO] run_cycle: SCAN S00 浜名湖5R S
2026-08-12 13:19:42,246 [INFO] run_cycle: run_cycle done: 1 notifications

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
    "c": 86
  },
  {
    "target": "primary",
    "ok": 1,
    "c": 86
  }
]
```

## Phase別通知記録 (24h)
{'final': 34, 'result': 14, 'scan': 38}

## アラート件数 (24h・種類別)
```
  ANOMALY_SCRAPER_FAILURE_BURST: 85
  FINAL_MISSING: 41
  CIRCUIT_BREAKER_NO_ACTION: 27
  CIRCUIT_BREAKER_TRIP: 22
  STRATEGY_CI_FAIL: 17
  ANOMALY_SCAN_FINAL_RATIO: 14
```

## 戦略別 ROI (7日)
| sid | n | hits | cost | payout | PL | ROI |
|---|---|---|---|---|---|---|
| S00 | 32 | 8 | 9,600 | 7,500 | -2,100 | 0.781 |
| S01_NAKAANA1 | 48 | 9 | 9,600 | 5,540 | -4,060 | 0.577 |
| S02_TETSUBAN | 18 | 11 | 3,600 | 3,340 | -260 | 0.928 |

## 直近アラート (24h・新しい順)
```
[13:19:42] ANOMALY_SCAN_FINAL_RATIO: {"abs_drop": 0.356, "baseline_mean": 0.818, "baseline_stdev": 0.082, "kind": "ANOMALY_SCAN_FINAL_RATIO", "today_ratio": 0.462, "today_scan_count": 13, "z_score": -4.32}
[13:17:19] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1120}
[13:16:34] CIRCUIT_BREAKER_TRIP: {"cost": 9600, "kind": "CIRCUIT_BREAKER_TRIP", "n": 48, "payout": 5540, "roi_7d": 0.577, "sid": "S01_NAKAANA1"}
[13:16:34] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1110}
[13:15:45] FINAL_MISSING: {"deadline": "2026-08-12T11:45:00+09:00", "kind": "FINAL_MISSING", "nid": "2026081202031145", "sid": "S00"}
[13:15:45] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1079}
[13:14:43] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1082}
[13:13:20] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1107}
[13:12:22] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1108}
[13:11:46] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1105}
```

## 本日残レース: 122件

## 本日nidレジャー（ID単位完遂突合せ）
- race_schedule: 180件 登録 / 58件 締切済
- 通知発射: scan=13 nid / final=9 nid / result=2 nid
- predictions: 4 / うち結果DB記録済: 3
- ✅ 結果DBあるが通知未発射: 0件 `tools/backfill_result_notifications.py` で救済可
- 🔴 scan後final無しのまま締切: 5件（FINAL_MISSING の温床）

## 直近送信失敗 (24h)
```
```

## 最新 predictions サンプル (計算spot-check用)
| sid | race | bt | combo | p | odds | ev | bet | at |
|---|---|---|---|---|---|---|---|---|
| S01_NAKAANA1 | 223R | win | 1 | 0.5990 | 3.1 | 1.86 | 200 | scan=- drift=- | 13:16:19 |
| S00 | 032R | win | 1 | 0.4980 | 4.0 | 1.99 | 300 | scan=- drift=- | 11:39:18 |
| S01_NAKAANA1 | 032R | win | 1 | 0.4980 | 3.7 | 1.84 | 200 | scan=- drift=- | 11:38:19 |
| S02_TETSUBAN | 211R | win | 1 | 0.5334 | 2.1 | 1.12 | 200 | scan=- drift=- | 08:29:19 |
| S02_TETSUBAN | 079R | win | 1 | 0.4989 | 2.6 | 1.30 | 200 | scan=2.5 drift=+4.0% | 19:08:19 |
| S01_NAKAANA1 | 194R | win | 1 | 0.5990 | 4.0 | 2.40 | 200 | scan=- drift=- | 19:00:46 |
| S02_TETSUBAN | 208R | win | 1 | 0.5334 | 2.0 | 1.07 | 200 | scan=2.1 drift=-4.8% | 18:43:29 |
| S02_TETSUBAN | 076R | win | 1 | 0.5174 | 2.3 | 1.19 | 200 | scan=- drift=- | 17:33:45 |
| S02_TETSUBAN | 0512R | win | 1 | 0.4989 | 2.5 | 1.25 | 200 | scan=2.4 drift=+4.2% | 17:22:36 |
| S01_NAKAANA1 | 074R | win | 1 | 0.5891 | 3.7 | 2.18 | 200 | scan=3.2 drift=+15.6% | 16:40:45 |

## オッズドリフト統計 (7日)

| bt | n | avg | min | max | down10 | collapse(≤-30%) | any_large(≥10%) |
|---|---|---|---|---|---|---|---|
| win | 61 | +7.9% | -53.3% | +287.7% | 18 | 8 | 41 |

## 校正テーブル合格状況

- total: 27 グループ
- passed: 19
- failed: 8 — `2f|4, 2f|5, 3f|2, 3f|3, 3f|4, 3t|1, 3t|4, 3t|5`
- 主力グループ状態: ✅ (全12グループ合格)

## SRE Golden Signals (24h)

| Signal | Value |
|---|---|
| **Latency** (scan→final avg) | 443.5s |
| **Latency** (scan→final max) | 616.7s |
| **Traffic** (notifications 24h) | 86 |
| **Errors** (send fail rate) | ✅ 0.0% |
| **Saturation** (S00) | 300円 used |
| **Saturation** (S01_NAKAANA1) | 400円 used |
| **Saturation** (S02_TETSUBAN) | 200円 used |

## 信ぴょう性メトリクス（予測精度の証拠）

### bt別: 予測確率 vs 実的中率
| bt | n | 予測avg | 実的中率 | 校正誤差 | 過信度 | Brier |
|---|---|---|---|---|---|---|
| win | 397 | 0.4680 | 0.2720 | +0.1960 | 🟡+42% | 0.2362 |

### 戦略別: 校正精度 + Brier Skill Score
| sid | bt | n | pred | actual | Brier | BSS | ROI |
|---|---|---|---|---|---|---|---|
| S00 | win | 163 | 0.4201 | 0.2209 | 0.2246 | 🔴-0.31 | 0.623 |
| S01_NAKAANA1 | win | 165 | 0.4893 | 0.2121 | 0.2465 | 🔴-0.48 | 0.662 |
| S02_TETSUBAN | win | 69 | 0.5303 | 0.5362 | 0.2388 | ✅+0.04 | 0.903 |

### 確率デシル別: 校正カーブ
| 確率帯 | n | 予測avg | 実的中率 | gap |
|---|---|---|---|---|
| 0.10-0.15 | 11 | 0.1216 | 0.1818 | 🔴-0.0602 |
| 0.15-0.20 | 10 | 0.1843 | 0.1000 | 🔴+0.0843 |
| 0.20-0.30 | 8 | 0.2235 | 0.3750 | 🔴-0.1515 |
| 0.30-0.50 | 153 | 0.4212 | 0.2157 | 🔴+0.2055 |
| 0.50+ | 214 | 0.5434 | 0.3224 | 🔴+0.2210 |

## Settlement Ratio データ品質

- 学習済み: 4バンド / fallback: 13バンド
| bt | odds帯 | source | n | ratio |
|---|---|---|---|---|
| win | <3.0 | ✅learned | 107 | 0.773 |
| win | <5.0 | ✅learned | 181 | 0.725 |
| win | <10.0 | ✅learned | 91 | 0.451 |
| win | <20.0 | ✅learned | 30 | 0.227 |
| win | <50.0 | ⚠️fallback | 6 | 0.1 |
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
_auto-generated by claude_snapshot.py at 2026-08-12T13:20:01.968176+09:00_