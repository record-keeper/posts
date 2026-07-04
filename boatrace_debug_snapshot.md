# ClaudeDebug スナップショット

## 🔴 現状: RED

**生成**: 2026-07-04T15:40:01.814584+09:00

### 次に取るべきアクション
> RED最優先: STRATEGY_CI_FAIL×17 (24h) → ログ/DB確認

### 検出された問題
- 🟡 FINAL_MISSING×21 (24h)
- 🔴 STRATEGY_CI_FAIL×17 (24h)
- 🔴 CIRCUIT_BREAKER_TRIP×8 (24h)
- 🔴 PSI_DRIFT_DETECTED×4 (24h)
- 🟡 LARGE_ODDS_DRIFT×1 (24h)
- 🔴 alert_manager dispatch 失敗確定 1件（手動確認必要）

---

## 🔧 AI デバッグキュー（このClaudeが対処）

### 🔴 CIRCUIT_BREAKER_NO_ACTION  ×70  [2026-07-04T15:05:07]
- key: `CIRCUIT_BREAKER_NO_ACTION|`
- **FIX**: CIRCUIT_BREAKER_TRIP 発動済なのに strategies.json で enabled のまま。enabled:false に切替 or 復旧条件満たしたか確認

### 🔴 STRATEGY_CI_FAIL  ×35  [2026-07-04T15:05:07]
- key: `STRATEGY_CI_FAIL|`
- **FIX**: grid戦略のOOS CI下限<1.0→論文基準で赤字リスク。strategies.json確認

### 🔴 CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION  ×2  [2026-07-04T15:00:04]
- key: `CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION|戦略 S00 が TRIP してるが enabled のまま`
- **FIX**: CIRCUIT_BREAKER_TRIP 戦略が enabled のまま。enabled:false に

### 🔴 CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION  ×2  [2026-07-04T15:00:04]
- key: `CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION|戦略 S02_TETSUBAN が TRIP してるが enabled のまま`
- **FIX**: CIRCUIT_BREAKER_TRIP 戦略が enabled のまま。enabled:false に

### 🟡 ANOMALY_SCRAPER_FAILURE_BURST  ×56  [2026-07-04T12:42:08]
- key: `ANOMALY_SCRAPER_FAILURE_BURST|`
- **FIX**: 直近1h でscraper 3-retry 全敗多発。boatrace.jp 側timeout / IP ban / DDoS

### 🟡 ANOMALY_SCAN_FINAL_RATIO  ×14  [2026-07-04T12:35:21]
- key: `ANOMALY_SCAN_FINAL_RATIO|`
- **FIX**: scan→final成立率が7日baselineから2σ逸脱。scan/final window設定・odds取得タイミング

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-07-04T06:00:14]
- key: `INSUFFICIENT_SAMPLE|S00: n=168<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-07-04T06:00:14]
- key: `INSUFFICIENT_SAMPLE|S02_TETSUBAN: n=77<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### 🟡 ORPHAN_SCAN  ×1  [2026-07-04T06:00:14]
- key: `ORPHAN_SCAN|154 件の scan に final/retreat 追従無し`
- **FIX**: scan 後 final も retreat も無い→当該レースの final 窓が短すぎ/fetch 失敗

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-07-04T06:00:14]
- key: `INSUFFICIENT_SAMPLE|S01_NAKAANA1: n=137<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ DRIFT_BUCKET  ×1  [2026-07-04T06:00:14]
- key: `DRIFT_BUCKET|drift +10%〜+30%: n=25 hit%=32.0% ROI=1.06 (コスト 6,100/回収 6,490)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-07-04T06:00:14]
- key: `DRIFT_BUCKET|drift ≥+30%: n=30 hit%=23.3% ROI=0.51 (コスト 8,400/回収 4,310)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ CALIBRATION_LIVE  ×1  [2026-07-04T06:00:14]
- key: `CALIBRATION_LIVE|decile 0.30-0.40: n=22 pred=0.3216 actual=0.1818 gap=+0.1397`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ DRIFT_BUCKET  ×1  [2026-07-04T06:00:14]
- key: `DRIFT_BUCKET|drift ≤-30%: n=36 hit%=27.8% ROI=0.85 (コスト 10,500/回収 8,940)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ ROI_STAT  ×1  [2026-07-04T06:00:14]
- key: `ROI_STAT|S00: n=168 hit%=26.8% hit_CI[Bonf]=[18.2,37.6]% ROI=0.72 ROI_boot95=[0.53,0.94]`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-07-04T06:00:14]
- key: `ROI_STAT|S01_NAKAANA1: n=137 hit%=31.4% hit_CI[Bonf]=[21.3,43.6]% ROI=0.85 ROI_boot95=[0.`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-07-04T06:00:14]
- key: `ROI_STAT|S02_TETSUBAN: n=77 hit%=32.5% hit_CI[Bonf]=[19.4,48.9]% ROI=0.54 ROI_boot95=[0.3`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ DRIFT_BUCKET  ×1  [2026-07-04T06:00:14]
- key: `DRIFT_BUCKET|drift -30%〜-10%: n=41 hit%=24.4% ROI=0.61 (コスト 9,700/回収 5,900)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-07-04T06:00:14]
- key: `DRIFT_BUCKET|drift -10%〜+10%: n=91 hit%=29.7% ROI=0.71 (コスト 21,300/回収 15,180)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ CALIBRATION_LIVE  ×1  [2026-07-04T06:00:14]
- key: `CALIBRATION_LIVE|bt=win: n=382 pred=0.4791 actual=0.2958 error=+0.1833 (+38%) brier=0.2396 [OVERC`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用


以下、詳細セクション（通常読み飛ばし可）

## 環境・コード状態
- git_sha: `<error: Command '['git', '-C', '/opt/boa` dirty=True
- config.json md5: `eb532e851a30cd2f7e69bdf0dfca3f2b`
- strategies.json md5: `06b22dd935785e7947bf9c0f170b69a3`
- numpy=2.4.4 lightgbm=4.6.0 scipy=1.17.1
- **calibration_applied**: True ← predictor.py が校正を呼んでるか
- DB: 6.71MB / last modified 2026-07-04T15:39:35.977277+09:00

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
6-07-04 15:39:19,847 [INFO] scraper: odds2f: 15/15 parsed
2026-07-04 15:39:20,921 [INFO] scraper: odds_win: 3/6 parsed
2026-07-04 15:39:20,922 [INFO] scraper: fetch_race 08/11: boats=6 odds=188/191
2026-07-04 15:39:20,932 [INFO] predictor: CALIBRATION_MODE=on
2026-07-04 15:39:20,932 [INFO] predictor: combos: {'win': 3, '2t': 30, '3t': 120}
2026-07-04 15:39:20,940 [INFO] run_cycle: fetched 08/11 [final]: 153 combos
2026-07-04 15:39:24,374 [INFO] scraper: odds3t: 120/120 parsed
2026-07-04 15:39:25,468 [INFO] scraper: odds3f: 20/20 parsed
2026-07-04 15:39:26,543 [INFO] scraper: odds2t: 30/30 parsed
2026-07-04 15:39:26,544 [INFO] scraper: odds2f: 14/15 parsed
2026-07-04 15:39:27,641 [INFO] scraper: odds_win: 6/6 parsed
2026-07-04 15:39:27,641 [INFO] scraper: fetch_race 13/11: boats=6 odds=190/191
2026-07-04 15:39:27,650 [INFO] predictor: CALIBRATION_MODE=on
2026-07-04 15:39:27,650 [INFO] predictor: combos: {'win': 6, '2t': 30, '3t': 120}
2026-07-04 15:39:27,658 [INFO] run_cycle: fetched 13/11 [scan]: 156 combos
2026-07-04 15:39:31,272 [INFO] scraper: odds3t: 120/120 parsed
2026-07-04 15:39:32,367 [INFO] scraper: odds3f: 20/20 parsed
2026-07-04 15:39:33,479 [INFO] scraper: odds2t: 30/30 parsed
2026-07-04 15:39:33,480 [INFO] scraper: odds2f: 15/15 parsed
2026-07-04 15:39:34,581 [INFO] scraper: odds_win: 5/6 parsed
2026-07-04 15:39:34,581 [INFO] scraper: fetch_race 09/11: boats=6 odds=190/191
2026-07-04 15:39:34,589 [INFO] predictor: CALIBRATION_MODE=on
2026-07-04 15:39:34,591 [INFO] predictor: combos: {'win': 5, '2t': 30, '3t': 120}
2026-07-04 15:39:34,600 [INFO] run_cycle: fetched 09/11 [scan]: 155 combos
2026-07-04 15:39:34,704 [INFO] race_id: notif: nid=2026070409111549 sid=S00 phase=scan rank=SS
2026-07-04 15:39:35,019 [INFO] notifier: Discord notify OK (status=204)
2026-07-04 15:39:35,402 [INFO] notifier: Discord notify OK (status=204)
2026-07-04 15:39:35,736 [INFO] run_cycle: SCAN S00 津11R SS
2026-07-04 15:39:35,850 [INFO] run_cycle: run_cycle done: 1 notifications

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
    "c": 77
  },
  {
    "target": "primary",
    "ok": 1,
    "c": 77
  }
]
```

## Phase別通知記録 (24h)
{'final': 30, 'result': 14, 'scan': 33}

## アラート件数 (24h・種類別)
```
  ANOMALY_SCRAPER_FAILURE_BURST: 121
  CIRCUIT_BREAKER_NO_ACTION: 34
  FINAL_MISSING: 21
  STRATEGY_CI_FAIL: 17
  ANOMALY_SCAN_FINAL_RATIO: 14
  CIRCUIT_BREAKER_TRIP: 8
  PSI_DRIFT_DETECTED: 4
  LARGE_ODDS_DRIFT: 1
```

## 戦略別 ROI (7日)
| sid | n | hits | cost | payout | PL | ROI |
|---|---|---|---|---|---|---|
| S00 | 35 | 11 | 10,500 | 8,190 | -2,310 | 0.78 |
| S01_NAKAANA1 | 34 | 13 | 6,800 | 6,320 | -480 | 0.929 |
| S02_TETSUBAN | 22 | 10 | 4,400 | 3,400 | -1,000 | 0.773 |

## 直近アラート (24h・新しい順)
```
[15:39:35] FINAL_MISSING: {"deadline": "2026-07-04T13:08:00+09:00", "kind": "FINAL_MISSING", "nid": "2026070409061308", "sid": "S00"}
[15:26:21] FINAL_MISSING: {"deadline": "2026-07-04T13:55:00+09:00", "kind": "FINAL_MISSING", "nid": "2026070404051355", "sid": "S00"}
[15:20:38] FINAL_MISSING: {"deadline": "2026-07-04T10:47:00+09:00", "kind": "FINAL_MISSING", "nid": "2026070421061047", "sid": "S00"}
[15:05:07] STRATEGY_CI_FAIL: {"ci_lo": null, "kind": "STRATEGY_CI_FAIL", "sid": "S02_TETSUBAN"}
[15:05:07] CIRCUIT_BREAKER_NO_ACTION: {"kind": "CIRCUIT_BREAKER_NO_ACTION", "sid": "S02_TETSUBAN"}
[15:05:07] CIRCUIT_BREAKER_NO_ACTION: {"kind": "CIRCUIT_BREAKER_NO_ACTION", "sid": "S00"}
[15:00:25] FINAL_MISSING: {"deadline": "2026-07-04T11:29:00+09:00", "kind": "FINAL_MISSING", "nid": "2026070413031129", "sid": "S01_NAKAANA1"}
[14:40:31] FINAL_MISSING: {"deadline": "2026-07-04T12:09:00+09:00", "kind": "FINAL_MISSING", "nid": "2026070409041209", "sid": "S00"}
[14:39:22] FINAL_MISSING: {"deadline": "2026-07-04T13:08:00+09:00", "kind": "FINAL_MISSING", "nid": "2026070409061308", "sid": "S00"}
[14:25:41] FINAL_MISSING: {"deadline": "2026-07-04T13:55:00+09:00", "kind": "FINAL_MISSING", "nid": "2026070404051355", "sid": "S00"}
```

## 本日残レース: 63件

## 本日nidレジャー（ID単位完遂突合せ）
- race_schedule: 168件 登録 / 105件 締切済
- 通知発射: scan=25 nid / final=20 nid / result=8 nid
- predictions: 10 / うち結果DB記録済: 8
- ✅ 結果DBあるが通知未発射: 0件 `tools/backfill_result_notifications.py` で救済可
- 🔴 scan後final無しのまま締切: 7件（FINAL_MISSING の温床）

## 直近送信失敗 (24h)
```
```

## 最新 predictions サンプル (計算spot-check用)
| sid | race | bt | combo | p | odds | ev | bet | at |
|---|---|---|---|---|---|---|---|---|
| S01_NAKAANA1 | 011R | win | 1 | 0.5123 | 4.1 | 2.10 | 200 | scan=3.5 drift=+17.1% | 15:25:21 |
| S02_TETSUBAN | 0910R | win | 1 | 0.5729 | 2.2 | 1.26 | 200 | scan=2.2 drift=+0.0% | 15:13:33 |
| S02_TETSUBAN | 138R | win | 1 | 0.5891 | 2.0 | 1.18 | 200 | scan=- drift=- | 14:03:22 |
| S00 | 223R | win | 1 | 0.5269 | 18.7 | 9.85 | 300 | scan=- drift=- | 13:07:21 |
| S00 | 222R | win | 1 | 0.5050 | 4.2 | 2.12 | 300 | scan=5.2 drift=-19.2% | 12:37:33 |
| S01_NAKAANA1 | 188R | win | 1 | 0.5123 | 3.1 | 1.59 | 200 | scan=4.2 drift=-26.2% | 12:00:26 |
| S00 | 218R | win | 1 | 0.5123 | 8.8 | 4.51 | 300 | scan=6.7 drift=+31.3% | 11:46:44 |
| S01_NAKAANA1 | 237R | win | 1 | 0.4111 | 4.6 | 1.89 | 200 | scan=4.6 drift=+0.0% | 11:19:31 |
| S00 | 183R | win | 1 | 0.5123 | 5.0 | 2.56 | 300 | scan=- drift=- | 09:35:33 |
| S00 | 233R | win | 1 | 0.5334 | 5.2 | 2.77 | 300 | scan=4.5 drift=+15.6% | 09:28:21 |

## オッズドリフト統計 (7日)

| bt | n | avg | min | max | down10 | collapse(≤-30%) | any_large(≥10%) |
|---|---|---|---|---|---|---|---|
| win | 58 | +7.5% | -68.9% | +584.6% | 19 | 7 | 31 |

## 校正テーブル合格状況

- total: 27 グループ
- passed: 19
- failed: 8 — `2f|4, 2f|5, 3f|2, 3f|3, 3f|4, 3t|1, 3t|4, 3t|5`
- 主力グループ状態: ✅ (全12グループ合格)

## SRE Golden Signals (24h)

| Signal | Value |
|---|---|
| **Latency** (scan→final avg) | 471.8s |
| **Latency** (scan→final max) | 604.6s |
| **Traffic** (notifications 24h) | 77 |
| **Errors** (send fail rate) | ✅ 0.0% |
| **Saturation** (S00) | 1,500円 used |
| **Saturation** (S01_NAKAANA1) | 600円 used |
| **Saturation** (S02_TETSUBAN) | 400円 used |

## 信ぴょう性メトリクス（予測精度の証拠）

### bt別: 予測確率 vs 実的中率
| bt | n | 予測avg | 実的中率 | 校正誤差 | 過信度 | Brier |
|---|---|---|---|---|---|---|
| win | 380 | 0.4796 | 0.3053 | +0.1744 | 🟡+36% | 0.2399 |

### 戦略別: 校正精度 + Brier Skill Score
| sid | bt | n | pred | actual | Brier | BSS | ROI |
|---|---|---|---|---|---|---|---|
| S00 | win | 168 | 0.4424 | 0.2798 | 0.2239 | 🔴-0.11 | 0.74 |
| S01_NAKAANA1 | win | 138 | 0.4918 | 0.3188 | 0.2446 | 🔴-0.13 | 0.86 |
| S02_TETSUBAN | win | 74 | 0.5416 | 0.3378 | 0.2673 | 🔴-0.19 | 0.565 |

### 確率デシル別: 校正カーブ
| 確率帯 | n | 予測avg | 実的中率 | gap |
|---|---|---|---|---|
| 0.15-0.20 | 7 | 0.1746 | 0.4286 | 🔴-0.2540 |
| 0.20-0.30 | 14 | 0.2291 | 0.0714 | 🔴+0.1577 |
| 0.30-0.50 | 132 | 0.4226 | 0.2727 | 🔴+0.1499 |
| 0.50+ | 224 | 0.5435 | 0.3393 | 🔴+0.2042 |

## Settlement Ratio データ品質

- 学習済み: 4バンド / fallback: 13バンド
| bt | odds帯 | source | n | ratio |
|---|---|---|---|---|
| win | <3.0 | ✅learned | 56 | 0.74 |
| win | <5.0 | ✅learned | 113 | 0.716 |
| win | <10.0 | ✅learned | 65 | 0.479 |
| win | <20.0 | ✅learned | 19 | 0.212 |
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
_auto-generated by claude_snapshot.py at 2026-07-04T15:40:01.814584+09:00_