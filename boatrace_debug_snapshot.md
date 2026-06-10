# ClaudeDebug スナップショット

## 🔴 現状: RED

**生成**: 2026-06-10T09:50:01.889273+09:00

### 次に取るべきアクション
> RED最優先: CIRCUIT_BREAKER_TRIP×71 (24h) → ログ/DB確認

### 検出された問題
- 🔴 CIRCUIT_BREAKER_TRIP×71 (24h)
- 🔴 CALIBRATION_DRIFT×32 (24h)
- 🟡 FINAL_MISSING×23 (24h)
- 🔴 STRATEGY_CI_FAIL×17 (24h)
- 🔴 PSI_DRIFT_DETECTED×6 (24h)
- 🟡 LARGE_ODDS_DRIFT×1 (24h)
- 🔴 alert_manager dispatch 失敗確定 1件（手動確認必要）

---

## 🔧 AI デバッグキュー（このClaudeが対処）

### 🔴 CALIBRATION_DRIFT  ×49  [2026-06-10T09:01:06]
- key: `CALIBRATION_DRIFT|`
- **FIX**: 予測確率が実的中率から50%以上乖離→isotonic_calibration.json 再生成 or モデル再学習が必要。EV計算が膨張中

### 🔴 CIRCUIT_BREAKER_TRIP  ×147  [2026-06-10T09:01:06]
- key: `CIRCUIT_BREAKER_TRIP|`
- **FIX**: 7日ROI<0.7→戦略を enabled:false にして原因調査。校正ドリフトか市場変化を確認

### 🔴 CIRCUIT_BREAKER_NO_ACTION  ×147  [2026-06-10T09:01:06]
- key: `CIRCUIT_BREAKER_NO_ACTION|`
- **FIX**: CIRCUIT_BREAKER_TRIP 発動済なのに strategies.json で enabled のまま。enabled:false に切替 or 復旧条件満たしたか確認

### 🔴 STRATEGY_CI_FAIL  ×49  [2026-06-10T09:01:06]
- key: `STRATEGY_CI_FAIL|`
- **FIX**: grid戦略のOOS CI下限<1.0→論文基準で赤字リスク。strategies.json確認

### 🔴 CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION  ×2  [2026-06-10T09:00:04]
- key: `CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION|戦略 S00 が TRIP してるが enabled のまま`
- **FIX**: CIRCUIT_BREAKER_TRIP 戦略が enabled のまま。enabled:false に

### 🔴 CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION  ×2  [2026-06-10T09:00:04]
- key: `CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION|戦略 S01_NAKAANA1 が TRIP してるが enabled のまま`
- **FIX**: CIRCUIT_BREAKER_TRIP 戦略が enabled のまま。enabled:false に

### 🔴 CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION  ×2  [2026-06-10T09:00:04]
- key: `CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION|戦略 S02_TETSUBAN が TRIP してるが enabled のまま`
- **FIX**: CIRCUIT_BREAKER_TRIP 戦略が enabled のまま。enabled:false に

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-06-10T06:00:13]
- key: `INSUFFICIENT_SAMPLE|S02_TETSUBAN: n=83<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ DRIFT_BUCKET  ×1  [2026-06-10T06:00:13]
- key: `DRIFT_BUCKET|drift +10%〜+30%: n=37 hit%=27.0% ROI=1.00 (コスト 8,400/回収 8,380)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ CALIBRATION_LIVE  ×1  [2026-06-10T06:00:13]
- key: `CALIBRATION_LIVE|decile 0.10-0.15: n=6 pred=0.1254 actual=0.1667 gap=-0.0412`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-06-10T06:00:13]
- key: `CALIBRATION_LIVE|decile 0.20-0.30: n=6 pred=0.2216 actual=0.3333 gap=-0.1117`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-06-10T06:00:13]
- key: `CALIBRATION_LIVE|decile 0.15-0.20: n=5 pred=0.1918 actual=0.2000 gap=-0.0082`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-06-10T06:00:13]
- key: `ROI_STAT|S00: n=153 hit%=25.5% hit_CI[Bonf]=[16.8,36.7]% ROI=0.78 ROI_boot95=[0.53,1.07]`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-06-10T06:00:13]
- key: `INSUFFICIENT_SAMPLE|S00: n=153<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ ROI_STAT  ×1  [2026-06-10T06:00:13]
- key: `ROI_STAT|S01_NAKAANA1: n=143 hit%=28.7% hit_CI[Bonf]=[19.2,40.5]% ROI=0.70 ROI_boot95=[0.`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-06-10T06:00:13]
- key: `INSUFFICIENT_SAMPLE|S01_NAKAANA1: n=143<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ ROI_STAT  ×1  [2026-06-10T06:00:13]
- key: `ROI_STAT|S02_TETSUBAN: n=83 hit%=39.8% hit_CI[Bonf]=[25.9,55.5]% ROI=0.68 ROI_boot95=[0.4`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### 🟡 ORPHAN_SCAN  ×1  [2026-06-10T06:00:13]
- key: `ORPHAN_SCAN|142 件の scan に final/retreat 追従無し`
- **FIX**: scan 後 final も retreat も無い→当該レースの final 窓が短すぎ/fetch 失敗

### ℹ️ DRIFT_BUCKET  ×1  [2026-06-10T06:00:13]
- key: `DRIFT_BUCKET|drift ≤-30%: n=35 hit%=31.4% ROI=0.86 (コスト 10,300/回収 8,880)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-06-10T06:00:13]
- key: `DRIFT_BUCKET|drift -30%〜-10%: n=36 hit%=22.2% ROI=0.47 (コスト 7,900/回収 3,690)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料


以下、詳細セクション（通常読み飛ばし可）

## 環境・コード状態
- git_sha: `<error: Command '['git', '-C', '/opt/boa` dirty=True
- config.json md5: `eb532e851a30cd2f7e69bdf0dfca3f2b`
- strategies.json md5: `06b22dd935785e7947bf9c0f170b69a3`
- numpy=2.4.4 lightgbm=4.6.0 scipy=1.17.1
- **calibration_applied**: True ← predictor.py が校正を呼んでるか
- DB: 4.78MB / last modified 2026-06-10T09:49:06.688062+09:00

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
=5000
2026-06-10 09:48:06,325 [INFO] predictor: Models loaded OK
2026-06-10 09:48:17,361 [WARNING] scraper: fetch error (1/3): https://www.boatrace.jp/owpc/pc/race/racelist?rno=4&jcd=23&hd=20260610: HTTPSConnectionPool(host='www.boatrace.jp', port=443): Read timed out. (read timeout=10), retry in 1s
2026-06-10 09:48:29,912 [INFO] scraper: odds3t: 120/120 parsed
2026-06-10 09:48:31,000 [INFO] scraper: odds3f: 20/20 parsed
2026-06-10 09:48:32,096 [INFO] scraper: odds2t: 30/30 parsed
2026-06-10 09:48:32,097 [INFO] scraper: odds2f: 15/15 parsed
2026-06-10 09:48:33,258 [INFO] scraper: odds_win: 6/6 parsed
2026-06-10 09:48:33,259 [INFO] scraper: fetch_race 23/4: boats=6 odds=191/191
2026-06-10 09:48:33,271 [INFO] predictor: CALIBRATION_MODE=on
2026-06-10 09:48:33,271 [INFO] predictor: combos: {'win': 6, '2t': 30, '3t': 120}
2026-06-10 09:48:33,278 [INFO] run_cycle: fetched 23/4 [final]: 156 combos
2026-06-10 09:48:37,700 [INFO] scraper: odds3t: 120/120 parsed
2026-06-10 09:48:38,796 [INFO] scraper: odds3f: 20/20 parsed
2026-06-10 09:48:39,932 [INFO] scraper: odds2t: 30/30 parsed
2026-06-10 09:48:39,933 [INFO] scraper: odds2f: 12/15 parsed
2026-06-10 09:48:41,245 [INFO] scraper: odds_win: 3/6 parsed
2026-06-10 09:48:41,245 [INFO] scraper: fetch_race 18/4: boats=6 odds=185/191
2026-06-10 09:48:41,254 [INFO] predictor: CALIBRATION_MODE=on
2026-06-10 09:48:41,256 [INFO] predictor: combos: {'win': 3, '2t': 30, '3t': 120}
2026-06-10 09:48:41,262 [INFO] run_cycle: fetched 18/4 [scan]: 153 combos
2026-06-10 09:48:41,373 [INFO] run_cycle: run_cycle done: 0 notifications
2026-06-10 09:49:05,809 [INFO] run_cycle: === run_cycle 09:49:05 ===
2026-06-10 09:49:05,809 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-06-10 09:49:05,809 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-06-10 09:49:05,880 [INFO] predictor: Models loaded OK
2026-06-10 09:49:06,044 [INFO] run_cycle: run_cycle done: 0 notifications

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
    "c": 75
  },
  {
    "target": "primary",
    "ok": 1,
    "c": 75
  }
]
```

## Phase別通知記録 (24h)
{'final': 31, 'result': 18, 'scan': 26}

## アラート件数 (24h・種類別)
```
  CIRCUIT_BREAKER_TRIP: 71
  ANOMALY_SCRAPER_FAILURE_BURST: 51
  CIRCUIT_BREAKER_NO_ACTION: 51
  CALIBRATION_DRIFT: 32
  FINAL_MISSING: 23
  STRATEGY_CI_FAIL: 17
  ANOMALY_SCAN_FINAL_RATIO: 8
  PSI_DRIFT_DETECTED: 6
  LARGE_ODDS_DRIFT: 1
```

## 戦略別 ROI (7日)
| sid | n | hits | cost | payout | PL | ROI |
|---|---|---|---|---|---|---|
| S00 | 35 | 7 | 10,500 | 5,370 | -5,130 | 0.511 |
| S01_NAKAANA1 | 30 | 7 | 6,000 | 3,080 | -2,920 | 0.513 |
| S02_TETSUBAN | 27 | 7 | 5,400 | 1,980 | -3,420 | 0.367 |

## 直近アラート (24h・新しい順)
```
[09:01:05] STRATEGY_CI_FAIL: {"ci_lo": null, "kind": "STRATEGY_CI_FAIL", "sid": "S02_TETSUBAN"}
[09:01:05] CIRCUIT_BREAKER_TRIP: {"cost": 5400, "kind": "CIRCUIT_BREAKER_TRIP", "n": 27, "payout": 1980, "roi_7d": 0.367, "sid": "S02_TETSUBAN"}
[09:01:05] CIRCUIT_BREAKER_TRIP: {"cost": 6000, "kind": "CIRCUIT_BREAKER_TRIP", "n": 30, "payout": 3080, "roi_7d": 0.513, "sid": "S01_NAKAANA1"}
[09:01:05] CIRCUIT_BREAKER_TRIP: {"cost": 10500, "kind": "CIRCUIT_BREAKER_TRIP", "n": 35, "payout": 5370, "roi_7d": 0.511, "sid": "S00"}
[09:01:05] CALIBRATION_DRIFT: {"avg_actual": 0.2283, "avg_pred": 0.4862, "bt": "win", "kind": "CALIBRATION_DRIFT", "n": 92, "overconf_pct": 53.1}
[09:01:05] CIRCUIT_BREAKER_NO_ACTION: {"kind": "CIRCUIT_BREAKER_NO_ACTION", "sid": "S02_TETSUBAN"}
[09:01:05] CIRCUIT_BREAKER_NO_ACTION: {"kind": "CIRCUIT_BREAKER_NO_ACTION", "sid": "S01_NAKAANA1"}
[09:01:05] CIRCUIT_BREAKER_NO_ACTION: {"kind": "CIRCUIT_BREAKER_NO_ACTION", "sid": "S00"}
[08:00:38] STRATEGY_CI_FAIL: {"ci_lo": null, "kind": "STRATEGY_CI_FAIL", "sid": "S02_TETSUBAN"}
[08:00:38] CIRCUIT_BREAKER_TRIP: {"cost": 5400, "kind": "CIRCUIT_BREAKER_TRIP", "n": 27, "payout": 1980, "roi_7d": 0.367, "sid": "S02_TETSUBAN"}
```

## 本日残レース: 134件

## 本日nidレジャー（ID単位完遂突合せ）
- race_schedule: 144件 登録 / 10件 締切済
- 通知発射: scan=0 nid / final=0 nid / result=0 nid
- predictions: 0 / うち結果DB記録済: 0
- ✅ 結果DBあるが通知未発射: 0件 `tools/backfill_result_notifications.py` で救済可
- ✅ scan後final無しのまま締切: 0件（FINAL_MISSING の温床）

## 直近送信失敗 (24h)
```
```

## 最新 predictions サンプル (計算spot-check用)
| sid | race | bt | combo | p | odds | ev | bet | at |
|---|---|---|---|---|---|---|---|---|
| S02_TETSUBAN | 0711R | win | 1 | 0.5735 | 2.7 | 1.55 | 200 | scan=2.9 drift=-6.9% | 20:13:22 |
| S02_TETSUBAN | 078R | win | 1 | 0.5334 | 2.0 | 1.07 | 200 | scan=- drift=- | 18:52:32 |
| S02_TETSUBAN | 075R | win | 1 | 0.5476 | 2.0 | 1.10 | 200 | scan=2.1 drift=-4.8% | 17:34:21 |
| S01_NAKAANA1 | 155R | win | 1 | 0.5334 | 4.2 | 2.24 | 200 | scan=- drift=- | 17:21:31 |
| S00 | 074R | win | 1 | 0.5476 | 7.6 | 4.16 | 300 | scan=- drift=- | 17:10:24 |
| S00 | 073R | win | 1 | 0.4111 | 7.5 | 3.08 | 300 | scan=5.2 drift=+44.2% | 16:38:21 |
| S01_NAKAANA1 | 0510R | win | 1 | 0.5123 | 4.1 | 2.10 | 200 | scan=4.5 drift=-8.9% | 16:12:23 |
| S00 | 0510R | win | 1 | 0.5123 | 4.1 | 2.10 | 300 | scan=4.5 drift=-8.9% | 16:12:22 |
| S00 | 0910R | win | 1 | 0.5891 | 8.2 | 4.83 | 300 | scan=- drift=- | 15:10:25 |
| S01_NAKAANA1 | 058R | win | 1 | 0.4111 | 3.1 | 1.27 | 200 | scan=- drift=- | 15:05:33 |

## オッズドリフト統計 (7日)

| bt | n | avg | min | max | down10 | collapse(≤-30%) | any_large(≥10%) |
|---|---|---|---|---|---|---|---|
| win | 47 | +10.8% | -62.9% | +274.6% | 14 | 6 | 27 |

## 校正テーブル合格状況

- total: 27 グループ
- passed: 19
- failed: 8 — `2f|4, 2f|5, 3f|2, 3f|3, 3f|4, 3t|1, 3t|4, 3t|5`
- 主力グループ状態: ✅ (全12グループ合格)

## SRE Golden Signals (24h)

| Signal | Value |
|---|---|
| **Latency** (scan→final avg) | 496.2s |
| **Latency** (scan→final max) | 615.1s |
| **Traffic** (notifications 24h) | 75 |
| **Errors** (send fail rate) | ✅ 0.0% |

## 信ぴょう性メトリクス（予測精度の証拠）

### bt別: 予測確率 vs 実的中率
| bt | n | 予測avg | 実的中率 | 校正誤差 | 過信度 | Brier |
|---|---|---|---|---|---|---|
| win | 378 | 0.4684 | 0.2963 | +0.1722 | 🟡+37% | 0.2376 |

### 戦略別: 校正精度 + Brier Skill Score
| sid | bt | n | pred | actual | Brier | BSS | ROI |
|---|---|---|---|---|---|---|---|
| S00 | win | 153 | 0.4199 | 0.2549 | 0.2184 | 🔴-0.15 | 0.78 |
| S01_NAKAANA1 | win | 142 | 0.4883 | 0.2817 | 0.2431 | 🔴-0.20 | 0.701 |
| S02_TETSUBAN | win | 83 | 0.5241 | 0.3976 | 0.2637 | 🔴-0.10 | 0.684 |

### 確率デシル別: 校正カーブ
| 確率帯 | n | 予測avg | 実的中率 | gap |
|---|---|---|---|---|
| 0.10-0.15 | 6 | 0.1254 | 0.1667 | ✅-0.0412 |
| 0.15-0.20 | 5 | 0.1918 | 0.2000 | ✅-0.0082 |
| 0.20-0.30 | 6 | 0.2216 | 0.3333 | 🔴-0.1117 |
| 0.30-0.50 | 145 | 0.4207 | 0.2345 | 🔴+0.1862 |
| 0.50+ | 208 | 0.5412 | 0.3558 | 🔴+0.1854 |

## Settlement Ratio データ品質

- 学習済み: 4バンド / fallback: 13バンド
| bt | odds帯 | source | n | ratio |
|---|---|---|---|---|
| win | <3.0 | ✅learned | 35 | 0.736 |
| win | <5.0 | ✅learned | 65 | 0.727 |
| win | <10.0 | ✅learned | 42 | 0.51 |
| win | <20.0 | ✅learned | 13 | 0.212 |
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
_auto-generated by claude_snapshot.py at 2026-06-10T09:50:01.889273+09:00_