# ClaudeDebug スナップショット

## 🔴 現状: RED

**生成**: 2026-08-20T19:30:01.337618+09:00

### 次に取るべきアクション
> RED最優先: CIRCUIT_BREAKER_TRIP×20 (24h) → ログ/DB確認

### 検出された問題
- 🟡 FINAL_MISSING×63 (24h)
- 🔴 CIRCUIT_BREAKER_TRIP×20 (24h)
- 🔴 STRATEGY_CI_FAIL×17 (24h)
- 🟡 LARGE_ODDS_DRIFT×2 (24h)
- 🔴 alert_manager dispatch 失敗確定 1件（手動確認必要）

---

## 🔧 AI デバッグキュー（このClaudeが対処）

### 🔴 CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION  ×1  [2026-08-20T19:30:02]
- key: `CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION|戦略 S02_TETSUBAN が TRIP してるが enabled のまま`
- **FIX**: CIRCUIT_BREAKER_TRIP 戦略が enabled のまま。enabled:false に

### 🔴 CIRCUIT_BREAKER_TRIP  ×23  [2026-08-20T19:07:16]
- key: `CIRCUIT_BREAKER_TRIP|`
- **FIX**: 7日ROI<0.7→戦略を enabled:false にして原因調査。校正ドリフトか市場変化を確認

### 🔴 CIRCUIT_BREAKER_NO_ACTION  ×23  [2026-08-20T19:07:16]
- key: `CIRCUIT_BREAKER_NO_ACTION|`
- **FIX**: CIRCUIT_BREAKER_TRIP 発動済なのに strategies.json で enabled のまま。enabled:false に切替 or 復旧条件満たしたか確認

### 🔴 STRATEGY_CI_FAIL  ×23  [2026-08-20T19:07:16]
- key: `STRATEGY_CI_FAIL|`
- **FIX**: grid戦略のOOS CI下限<1.0→論文基準で赤字リスク。strategies.json確認

### 🟡 ANOMALY_SCRAPER_FAILURE_BURST  ×31  [2026-08-20T18:28:39]
- key: `ANOMALY_SCRAPER_FAILURE_BURST|`
- **FIX**: 直近1h でscraper 3-retry 全敗多発。boatrace.jp 側timeout / IP ban / DDoS

### 🟡 ANOMALY_BET_VOLUME_SPIKE  ×9  [2026-08-20T12:51:47]
- key: `ANOMALY_BET_VOLUME_SPIKE|`
- **FIX**: 本日のbet数が2σ急増。filter logic緩み・戦略追加・race_schedule異常

### 🟡 ANOMALY_SCAN_FINAL_RATIO  ×12  [2026-08-20T11:24:49]
- key: `ANOMALY_SCAN_FINAL_RATIO|`
- **FIX**: scan→final成立率が7日baselineから2σ逸脱。scan/final window設定・odds取得タイミング

### 🟡 ANOMALY_ODDS_SHIFT  ×24  [2026-08-20T10:59:34]
- key: `ANOMALY_ODDS_SHIFT|`
- **FIX**: odds 分布が2σシフト。scraper format変化・市場変動・戦略filterレンジ変更

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-08-20T06:00:19]
- key: `INSUFFICIENT_SAMPLE|S02_TETSUBAN: n=78<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-08-20T06:00:19]
- key: `INSUFFICIENT_SAMPLE|S00: n=165<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### 🟡 ORPHAN_SCAN  ×1  [2026-08-20T06:00:19]
- key: `ORPHAN_SCAN|194 件の scan に final/retreat 追従無し`
- **FIX**: scan 後 final も retreat も無い→当該レースの final 窓が短すぎ/fetch 失敗

### ℹ️ CALIBRATION_LIVE  ×1  [2026-08-20T06:00:19]
- key: `CALIBRATION_LIVE|decile 0.10-0.15: n=9 pred=0.1189 actual=0.1111 gap=+0.0078`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-08-20T06:00:19]
- key: `INSUFFICIENT_SAMPLE|S01_NAKAANA1: n=173<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ ROI_STAT  ×1  [2026-08-20T06:00:19]
- key: `ROI_STAT|S00: n=165 hit%=25.5% hit_CI[Bonf]=[17.0,36.3]% ROI=0.79 ROI_boot95=[0.54,1.08]`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-08-20T06:00:19]
- key: `ROI_STAT|S01_NAKAANA1: n=173 hit%=23.7% hit_CI[Bonf]=[15.7,34.1]% ROI=0.83 ROI_boot95=[0.`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-08-20T06:00:19]
- key: `ROI_STAT|S02_TETSUBAN: n=78 hit%=44.9% hit_CI[Bonf]=[29.9,60.8]% ROI=0.71 ROI_boot95=[0.5`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ DRIFT_BUCKET  ×1  [2026-08-20T06:00:19]
- key: `DRIFT_BUCKET|drift ≤-30%: n=35 hit%=22.9% ROI=0.67 (コスト 10,100/回収 6,770)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-08-20T06:00:19]
- key: `DRIFT_BUCKET|drift -30%〜-10%: n=32 hit%=37.5% ROI=1.22 (コスト 7,600/回収 9,290)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-08-20T06:00:19]
- key: `DRIFT_BUCKET|drift -10%〜+10%: n=90 hit%=27.8% ROI=0.88 (コスト 20,900/回収 18,410)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-08-20T06:00:19]
- key: `DRIFT_BUCKET|drift +10%〜+30%: n=49 hit%=24.5% ROI=0.48 (コスト 11,300/回収 5,420)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料


以下、詳細セクション（通常読み飛ばし可）

## 環境・コード状態
- git_sha: `<error: Command '['git', '-C', '/opt/boa` dirty=True
- config.json md5: `eb532e851a30cd2f7e69bdf0dfca3f2b`
- strategies.json md5: `06b22dd935785e7947bf9c0f170b69a3`
- numpy=2.4.4 lightgbm=4.6.0 scipy=1.17.1
- **calibration_applied**: True ← predictor.py が校正を呼んでるか
- DB: 11.01MB / last modified 2026-08-20T19:29:30.550595+09:00

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
00
2026-08-20 19:28:03,933 [INFO] predictor: Models loaded OK
2026-08-20 19:28:16,279 [INFO] scraper: odds3t: 120/120 parsed
2026-08-20 19:28:17,360 [INFO] scraper: odds3f: 20/20 parsed
2026-08-20 19:28:18,474 [INFO] scraper: odds2t: 30/30 parsed
2026-08-20 19:28:18,475 [INFO] scraper: odds2f: 14/15 parsed
2026-08-20 19:28:19,570 [INFO] scraper: odds_win: 6/6 parsed
2026-08-20 19:28:19,570 [INFO] scraper: fetch_race 24/5: boats=6 odds=190/191
2026-08-20 19:28:19,574 [INFO] predictor: CALIBRATION_MODE=on
2026-08-20 19:28:19,574 [INFO] predictor: combos: {'win': 6, '2t': 30, '3t': 120}
2026-08-20 19:28:19,578 [INFO] run_cycle: fetched 24/5 [final]: 156 combos
2026-08-20 19:28:19,759 [INFO] run_cycle: run_cycle done: 0 notifications
2026-08-20 19:29:04,311 [INFO] run_cycle: === run_cycle 19:29:04 ===
2026-08-20 19:29:04,312 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-08-20 19:29:04,312 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-08-20 19:29:04,365 [INFO] predictor: Models loaded OK
2026-08-20 19:29:15,423 [WARNING] scraper: fetch error (1/3): https://www.boatrace.jp/owpc/pc/race/racelist?rno=10&jcd=20&hd=20260820: HTTPSConnectionPool(host='www.boatrace.jp', port=443): Read timed out. (read timeout=10), retry in 1s
2026-08-20 19:29:26,948 [INFO] scraper: odds3t: 120/120 parsed
2026-08-20 19:29:28,064 [INFO] scraper: odds3f: 20/20 parsed
2026-08-20 19:29:29,170 [INFO] scraper: odds2t: 30/30 parsed
2026-08-20 19:29:29,171 [INFO] scraper: odds2f: 15/15 parsed
2026-08-20 19:29:30,263 [INFO] scraper: odds_win: 5/6 parsed
2026-08-20 19:29:30,263 [INFO] scraper: fetch_race 20/10: boats=6 odds=190/191
2026-08-20 19:29:30,267 [INFO] predictor: CALIBRATION_MODE=on
2026-08-20 19:29:30,267 [INFO] predictor: combos: {'win': 5, '2t': 30, '3t': 120}
2026-08-20 19:29:30,271 [INFO] run_cycle: fetched 20/10 [scan]: 155 combos
2026-08-20 19:29:30,386 [INFO] run_cycle: run_cycle done: 0 notifications

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
    "c": 83
  },
  {
    "target": "primary",
    "ok": 1,
    "c": 83
  }
]
```

## Phase別通知記録 (24h)
{'final': 34, 'result': 19, 'scan': 30}

## アラート件数 (24h・種類別)
```
  ANOMALY_SCRAPER_FAILURE_BURST: 135
  FINAL_MISSING: 63
  CIRCUIT_BREAKER_NO_ACTION: 21
  CIRCUIT_BREAKER_TRIP: 20
  STRATEGY_CI_FAIL: 17
  ANOMALY_SCAN_FINAL_RATIO: 8
  ANOMALY_BET_VOLUME_SPIKE: 3
  LARGE_ODDS_DRIFT: 2
  ANOMALY_ODDS_SHIFT: 1
```

## 戦略別 ROI (7日)
| sid | n | hits | cost | payout | PL | ROI |
|---|---|---|---|---|---|---|
| S00 | 43 | 17 | 12,900 | 19,140 | +6,240 | 1.484 |
| S01_NAKAANA1 | 49 | 19 | 9,800 | 14,180 | +4,380 | 1.447 |
| S02_TETSUBAN | 23 | 6 | 4,600 | 1,980 | -2,620 | 0.43 |

## 直近アラート (24h・新しい順)
```
[19:25:04] FINAL_MISSING: {"deadline": "2026-08-20T11:50:00+09:00", "kind": "FINAL_MISSING", "nid": "2026082021081150", "sid": "S00"}
[19:19:03] FINAL_MISSING: {"deadline": "2026-08-20T12:44:00+09:00", "kind": "FINAL_MISSING", "nid": "2026082002051244", "sid": "S00"}
[19:13:26] FINAL_MISSING: {"deadline": "2026-08-20T17:42:00+09:00", "kind": "FINAL_MISSING", "nid": "2026082004121742", "sid": "S00"}
[19:10:33] FINAL_MISSING: {"deadline": "2026-08-20T10:37:00+09:00", "kind": "FINAL_MISSING", "nid": "2026082013011037", "sid": "S00"}
[19:09:20] CIRCUIT_BREAKER_TRIP: {"cost": 4600, "kind": "CIRCUIT_BREAKER_TRIP", "n": 23, "payout": 1980, "roi_7d": 0.43, "sid": "S02_TETSUBAN"}
[19:06:20] STRATEGY_CI_FAIL: {"ci_lo": null, "kind": "STRATEGY_CI_FAIL", "sid": "S02_TETSUBAN"}
[19:06:20] FINAL_MISSING: {"deadline": "2026-08-20T09:32:00+09:00", "kind": "FINAL_MISSING", "nid": "2026082023030932", "sid": "S00"}
[19:06:20] CIRCUIT_BREAKER_NO_ACTION: {"kind": "CIRCUIT_BREAKER_NO_ACTION", "sid": "S02_TETSUBAN"}
[18:58:15] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 693}
[18:57:39] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 691}
```

## 本日残レース: 15件

## 本日nidレジャー（ID単位完遂突合せ）
- race_schedule: 168件 登録 / 153件 締切済
- 通知発射: scan=25 nid / final=28 nid / result=18 nid
- predictions: 19 / うち結果DB記録済: 19
- ✅ 結果DBあるが通知未発射: 0件 `tools/backfill_result_notifications.py` で救済可
- 🔴 scan後final無しのまま締切: 5件（FINAL_MISSING の温床）

## 直近送信失敗 (24h)
```
```

## 最新 predictions サンプル (計算spot-check用)
| sid | race | bt | combo | p | odds | ev | bet | at |
|---|---|---|---|---|---|---|---|---|
| S01_NAKAANA1 | 197R | win | 1 | 0.3177 | 3.3 | 1.05 | 200 | scan=- drift=- | 18:14:29 |
| S01_NAKAANA1 | 154R | win | 1 | 0.4989 | 3.0 | 1.50 | 200 | scan=- drift=- | 16:31:20 |
| S01_NAKAANA1 | 153R | win | 1 | 0.5891 | 3.0 | 1.77 | 200 | scan=- drift=- | 16:07:18 |
| S01_NAKAANA1 | 049R | win | 1 | 0.5476 | 4.8 | 2.63 | 200 | scan=- drift=- | 16:03:20 |
| S01_NAKAANA1 | 048R | win | 1 | 0.5891 | 3.9 | 2.30 | 200 | scan=4.4 drift=-11.4% | 15:28:18 |
| S01_NAKAANA1 | 191R | win | 1 | 0.5537 | 3.3 | 1.83 | 200 | scan=4.1 drift=-19.5% | 15:22:21 |
| S00 | 0210R | win | 1 | 0.5719 | 7.5 | 4.29 | 300 | scan=16.2 drift=-53.7% | 15:18:29 |
| S00 | 046R | win | 1 | 0.3647 | 8.0 | 2.92 | 300 | scan=10.1 drift=-20.8% | 14:23:19 |
| S00 | 044R | win | 1 | 0.5891 | 10.2 | 6.01 | 300 | scan=- drift=- | 13:21:20 |
| S00 | 043R | win | 1 | 0.5123 | 21.0 | 10.76 | 300 | scan=- drift=- | 12:51:31 |

## オッズドリフト統計 (7日)

| bt | n | avg | min | max | down10 | collapse(≤-30%) | any_large(≥10%) |
|---|---|---|---|---|---|---|---|
| win | 73 | +8.0% | -56.0% | +256.4% | 19 | 7 | 38 |

## 校正テーブル合格状況

- total: 27 グループ
- passed: 19
- failed: 8 — `2f|4, 2f|5, 3f|2, 3f|3, 3f|4, 3t|1, 3t|4, 3t|5`
- 主力グループ状態: ✅ (全12グループ合格)

## SRE Golden Signals (24h)

| Signal | Value |
|---|---|
| **Latency** (scan→final avg) | 486.6s |
| **Latency** (scan→final max) | 650.0s |
| **Traffic** (notifications 24h) | 83 |
| **Errors** (send fail rate) | ✅ 0.0% |
| **Saturation** (S00) | 2,400円 used |
| **Saturation** (S01_NAKAANA1) | 1,600円 used |
| **Saturation** (S02_TETSUBAN) | 600円 used |

## 信ぴょう性メトリクス（予測精度の証拠）

### bt別: 予測確率 vs 実的中率
| bt | n | 予測avg | 実的中率 | 校正誤差 | 過信度 | Brier |
|---|---|---|---|---|---|---|
| win | 424 | 0.4677 | 0.2995 | +0.1682 | 🟡+36% | 0.2398 |

### 戦略別: 校正精度 + Brier Skill Score
| sid | bt | n | pred | actual | Brier | BSS | ROI |
|---|---|---|---|---|---|---|---|
| S00 | win | 170 | 0.4154 | 0.2647 | 0.2243 | 🔴-0.15 | 0.809 |
| S01_NAKAANA1 | win | 175 | 0.4893 | 0.2629 | 0.2508 | 🔴-0.29 | 0.89 |
| S02_TETSUBAN | win | 79 | 0.5324 | 0.4557 | 0.2486 | 🔴-0.00 | 0.723 |

### 確率デシル別: 校正カーブ
| 確率帯 | n | 予測avg | 実的中率 | gap |
|---|---|---|---|---|
| 0.10-0.15 | 9 | 0.1189 | 0.1111 | ✅+0.0078 |
| 0.15-0.20 | 12 | 0.1800 | 0.1667 | ✅+0.0134 |
| 0.20-0.30 | 10 | 0.2255 | 0.3000 | 🔴-0.0745 |
| 0.30-0.50 | 153 | 0.4131 | 0.2549 | 🔴+0.1581 |
| 0.50+ | 238 | 0.5440 | 0.3445 | 🔴+0.1994 |

## Settlement Ratio データ品質

- 学習済み: 4バンド / fallback: 13バンド
| bt | odds帯 | source | n | ratio |
|---|---|---|---|---|
| win | <3.0 | ✅learned | 114 | 0.77 |
| win | <5.0 | ✅learned | 207 | 0.754 |
| win | <10.0 | ✅learned | 101 | 0.456 |
| win | <20.0 | ✅learned | 30 | 0.227 |
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
_auto-generated by claude_snapshot.py at 2026-08-20T19:30:01.337618+09:00_