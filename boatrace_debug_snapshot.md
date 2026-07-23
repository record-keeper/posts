# ClaudeDebug スナップショット

## 🔴 現状: RED

**生成**: 2026-07-23T16:30:01.375054+09:00

### 次に取るべきアクション
> RED最優先: CIRCUIT_BREAKER_TRIP×44 (24h) → ログ/DB確認

### 検出された問題
- 🟡 FINAL_MISSING×72 (24h)
- 🔴 CIRCUIT_BREAKER_TRIP×44 (24h)
- 🔴 STRATEGY_CI_FAIL×17 (24h)
- 🔴 CALIBRATION_DRIFT×1 (24h)
- 🔴 alert_manager dispatch 失敗確定 1件（手動確認必要）

---

## 🔧 AI デバッグキュー（このClaudeが対処）

### 🔴 CIRCUIT_BREAKER_TRIP  ×50  [2026-07-23T16:04:03]
- key: `CIRCUIT_BREAKER_TRIP|`
- **FIX**: 7日ROI<0.7→戦略を enabled:false にして原因調査。校正ドリフトか市場変化を確認

### 🔴 CIRCUIT_BREAKER_NO_ACTION  ×50  [2026-07-23T16:04:03]
- key: `CIRCUIT_BREAKER_NO_ACTION|`
- **FIX**: CIRCUIT_BREAKER_TRIP 発動済なのに strategies.json で enabled のまま。enabled:false に切替 or 復旧条件満たしたか確認

### 🔴 STRATEGY_CI_FAIL  ×25  [2026-07-23T16:04:03]
- key: `STRATEGY_CI_FAIL|`
- **FIX**: grid戦略のOOS CI下限<1.0→論文基準で赤字リスク。strategies.json確認

### 🔴 CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION  ×2  [2026-07-23T16:00:03]
- key: `CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION|戦略 S00 が TRIP してるが enabled のまま`
- **FIX**: CIRCUIT_BREAKER_TRIP 戦略が enabled のまま。enabled:false に

### 🔴 CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION  ×2  [2026-07-23T16:00:03]
- key: `CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION|戦略 S01_NAKAANA1 が TRIP してるが enabled のまま`
- **FIX**: CIRCUIT_BREAKER_TRIP 戦略が enabled のまま。enabled:false に

### 🟡 ANOMALY_SCAN_FINAL_RATIO  ×50  [2026-07-23T15:38:34]
- key: `ANOMALY_SCAN_FINAL_RATIO|`
- **FIX**: scan→final成立率が7日baselineから2σ逸脱。scan/final window設定・odds取得タイミング

### 🟡 ANOMALY_SCRAPER_FAILURE_BURST  ×51  [2026-07-23T15:37:19]
- key: `ANOMALY_SCRAPER_FAILURE_BURST|`
- **FIX**: 直近1h でscraper 3-retry 全敗多発。boatrace.jp 側timeout / IP ban / DDoS

### 🔴 CALIBRATION_DRIFT  ×4  [2026-07-23T10:57:27]
- key: `CALIBRATION_DRIFT|`
- **FIX**: 予測確率が実的中率から50%以上乖離→isotonic_calibration.json 再生成 or モデル再学習が必要。EV計算が膨張中

### 🟡 ORPHAN_SCAN  ×1  [2026-07-23T06:00:07]
- key: `ORPHAN_SCAN|166 件の scan に final/retreat 追従無し`
- **FIX**: scan 後 final も retreat も無い→当該レースの final 窓が短すぎ/fetch 失敗

### ℹ️ CALIBRATION_LIVE  ×1  [2026-07-23T06:00:07]
- key: `CALIBRATION_LIVE|decile 0.20-0.30: n=15 pred=0.2268 actual=0.2667 gap=-0.0399`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-07-23T06:00:07]
- key: `CALIBRATION_LIVE|decile 0.15-0.20: n=7 pred=0.1798 actual=0.4286 gap=-0.2488`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-07-23T06:00:07]
- key: `ROI_STAT|S00: n=179 hit%=27.4% hit_CI[Bonf]=[18.9,37.8]% ROI=0.72 ROI_boot95=[0.53,0.95]`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-07-23T06:00:07]
- key: `INSUFFICIENT_SAMPLE|S00: n=179<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ ROI_STAT  ×1  [2026-07-23T06:00:07]
- key: `ROI_STAT|S01_NAKAANA1: n=163 hit%=29.4% hit_CI[Bonf]=[20.3,40.6]% ROI=0.81 ROI_boot95=[0.`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-07-23T06:00:07]
- key: `INSUFFICIENT_SAMPLE|S01_NAKAANA1: n=163<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ ROI_STAT  ×1  [2026-07-23T06:00:07]
- key: `ROI_STAT|S02_TETSUBAN: n=71 hit%=47.9% hit_CI[Bonf]=[31.9,64.3]% ROI=0.96 ROI_boot95=[0.6`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-07-23T06:00:07]
- key: `INSUFFICIENT_SAMPLE|S02_TETSUBAN: n=71<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ DRIFT_BUCKET  ×1  [2026-07-23T06:00:07]
- key: `DRIFT_BUCKET|drift ≤-30%: n=31 hit%=25.8% ROI=0.57 (コスト 9,100/回収 5,160)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-07-23T06:00:07]
- key: `DRIFT_BUCKET|drift -30%〜-10%: n=46 hit%=32.6% ROI=0.89 (コスト 11,200/回収 9,990)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-07-23T06:00:07]
- key: `DRIFT_BUCKET|drift -10%〜+10%: n=79 hit%=35.4% ROI=0.85 (コスト 18,100/回収 15,350)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料


以下、詳細セクション（通常読み飛ばし可）

## 環境・コード状態
- git_sha: `<error: Command '['git', '-C', '/opt/boa` dirty=True
- config.json md5: `eb532e851a30cd2f7e69bdf0dfca3f2b`
- strategies.json md5: `06b22dd935785e7947bf9c0f170b69a3`
- numpy=2.4.4 lightgbm=4.6.0 scipy=1.17.1
- **calibration_applied**: True ← predictor.py が校正を呼んでるか
- DB: 8.46MB / last modified 2026-07-23T16:30:04.255977+09:00

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
t=5000
2026-07-23 16:28:03,352 [INFO] predictor: Models loaded OK
2026-07-23 16:28:14,415 [WARNING] scraper: fetch error (1/3): https://www.boatrace.jp/owpc/pc/race/racelist?rno=3&jcd=15&hd=20260723: HTTPSConnectionPool(host='www.boatrace.jp', port=443): Read timed out. (read timeout=10), retry in 1s
2026-07-23 16:28:25,907 [INFO] scraper: odds3t: 120/120 parsed
2026-07-23 16:28:27,034 [INFO] scraper: odds3f: 20/20 parsed
2026-07-23 16:28:28,156 [INFO] scraper: odds2t: 28/30 parsed
2026-07-23 16:28:28,157 [INFO] scraper: odds2f: 15/15 parsed
2026-07-23 16:28:29,255 [INFO] scraper: odds_win: 4/6 parsed
2026-07-23 16:28:29,255 [INFO] scraper: fetch_race 15/3: boats=6 odds=187/191
2026-07-23 16:28:29,258 [INFO] predictor: CALIBRATION_MODE=on
2026-07-23 16:28:29,259 [INFO] predictor: combos: {'win': 4, '2t': 28, '3t': 120}
2026-07-23 16:28:29,262 [INFO] run_cycle: fetched 15/3 [scan]: 152 combos
2026-07-23 16:28:29,463 [INFO] run_cycle: run_cycle done: 0 notifications
2026-07-23 16:29:03,504 [INFO] run_cycle: === run_cycle 16:29:03 ===
2026-07-23 16:29:03,504 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-07-23 16:29:03,504 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-07-23 16:29:03,531 [INFO] predictor: Models loaded OK
2026-07-23 16:29:16,373 [INFO] scraper: odds3t: 120/120 parsed
2026-07-23 16:29:17,509 [INFO] scraper: odds3f: 20/20 parsed
2026-07-23 16:29:18,590 [INFO] scraper: odds2t: 30/30 parsed
2026-07-23 16:29:18,591 [INFO] scraper: odds2f: 15/15 parsed
2026-07-23 16:29:19,727 [INFO] scraper: odds_win: 4/6 parsed
2026-07-23 16:29:19,727 [INFO] scraper: fetch_race 19/3: boats=6 odds=189/191
2026-07-23 16:29:19,730 [INFO] predictor: CALIBRATION_MODE=on
2026-07-23 16:29:19,730 [INFO] predictor: combos: {'win': 4, '2t': 30, '3t': 120}
2026-07-23 16:29:19,734 [INFO] run_cycle: fetched 19/3 [scan]: 154 combos
2026-07-23 16:29:19,833 [INFO] run_cycle: run_cycle done: 0 notifications

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
    "c": 66
  },
  {
    "target": "primary",
    "ok": 1,
    "c": 66
  }
]
```

## Phase別通知記録 (24h)
{'final': 24, 'result': 12, 'scan': 30}

## アラート件数 (24h・種類別)
```
  ANOMALY_SCRAPER_FAILURE_BURST: 272
  FINAL_MISSING: 72
  CIRCUIT_BREAKER_TRIP: 44
  CIRCUIT_BREAKER_NO_ACTION: 34
  ANOMALY_SCAN_FINAL_RATIO: 33
  STRATEGY_CI_FAIL: 17
  CALIBRATION_DRIFT: 1
```

## 戦略別 ROI (7日)
| sid | n | hits | cost | payout | PL | ROI |
|---|---|---|---|---|---|---|
| S00 | 45 | 10 | 13,500 | 8,640 | -4,860 | 0.64 |
| S01_NAKAANA1 | 40 | 7 | 8,000 | 5,220 | -2,780 | 0.652 |
| S02_TETSUBAN | 18 | 9 | 3,600 | 3,320 | -280 | 0.922 |

## 直近アラート (24h・新しい順)
```
[16:29:19] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1035}
[16:28:29] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1036}
[16:27:03] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1052}
[16:26:19] FINAL_MISSING: {"deadline": "2026-07-23T15:56:00+09:00", "kind": "FINAL_MISSING", "nid": "2026072301021556", "sid": "S00"}
[16:26:19] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1057}
[16:25:25] FINAL_MISSING: {"deadline": "2026-07-23T11:53:00+09:00", "kind": "FINAL_MISSING", "nid": "2026072323081153", "sid": "S00"}
[16:25:25] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 5, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1054}
[16:24:21] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 5, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1064}
[16:24:21] ANOMALY_SCAN_FINAL_RATIO: {"abs_drop": 0.246, "baseline_mean": 0.811, "baseline_stdev": 0.062, "kind": "ANOMALY_SCAN_FINAL_RATIO", "today_ratio": 0.565, "today_scan_count": 23, "z_score": -3.97}
[16:23:26] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 5, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1050}
```

## 本日残レース: 46件

## 本日nidレジャー（ID単位完遂突合せ）
- race_schedule: 156件 登録 / 110件 締切済
- 通知発射: scan=23 nid / final=19 nid / result=10 nid
- predictions: 11 / うち結果DB記録済: 10
- ✅ 結果DBあるが通知未発射: 0件 `tools/backfill_result_notifications.py` で救済可
- 🔴 scan後final無しのまま締切: 10件（FINAL_MISSING の温床）

## 直近送信失敗 (24h)
```
```

## 最新 predictions サンプル (計算spot-check用)
| sid | race | bt | combo | p | odds | ev | bet | at |
|---|---|---|---|---|---|---|---|---|
| S00 | 152R | win | 1 | 0.4111 | 4.1 | 1.69 | 300 | scan=- drift=- | 15:57:20 |
| S00 | 0911R | win | 1 | 0.4111 | 9.6 | 3.95 | 300 | scan=- drift=- | 15:43:18 |
| S01_NAKAANA1 | 056R | win | 1 | 0.4111 | 3.2 | 1.32 | 200 | scan=- drift=- | 14:01:29 |
| S02_TETSUBAN | 097R | win | 1 | 0.5476 | 2.0 | 1.10 | 200 | scan=- drift=- | 13:36:29 |
| S02_TETSUBAN | 054R | win | 1 | 0.5735 | 2.3 | 1.32 | 200 | scan=2.2 drift=+4.5% | 13:00:27 |
| S00 | 2310R | win | 1 | 0.4111 | 5.4 | 2.22 | 300 | scan=14.2 drift=-62.0% | 12:53:19 |
| S00 | 149R | win | 1 | 0.5735 | 12.1 | 6.94 | 300 | scan=6.7 drift=+80.6% | 12:24:19 |
| S00 | 032R | win | 1 | 0.1371 | 5.5 | 0.75 | 300 | scan=4.7 drift=+17.0% | 11:38:19 |
| S01_NAKAANA1 | 237R | win | 1 | 0.5891 | 3.9 | 2.30 | 200 | scan=4.2 drift=-7.1% | 11:19:20 |
| S02_TETSUBAN | 092R | win | 1 | 0.5719 | 2.3 | 1.32 | 200 | scan=- drift=- | 11:01:20 |

## オッズドリフト統計 (7日)

| bt | n | avg | min | max | down10 | collapse(≤-30%) | any_large(≥10%) |
|---|---|---|---|---|---|---|---|
| win | 52 | +21.8% | -83.7% | +628.9% | 20 | 9 | 39 |

## 校正テーブル合格状況

- total: 27 グループ
- passed: 19
- failed: 8 — `2f|4, 2f|5, 3f|2, 3f|3, 3f|4, 3t|1, 3t|4, 3t|5`
- 主力グループ状態: ✅ (全12グループ合格)

## SRE Golden Signals (24h)

| Signal | Value |
|---|---|
| **Latency** (scan→final avg) | 500.5s |
| **Latency** (scan→final max) | 618.7s |
| **Traffic** (notifications 24h) | 66 |
| **Errors** (send fail rate) | ✅ 0.0% |
| **Saturation** (S00) | 1,500円 used |
| **Saturation** (S01_NAKAANA1) | 400円 used |
| **Saturation** (S02_TETSUBAN) | 800円 used |

## 信ぴょう性メトリクス（予測精度の証拠）

### bt別: 予測確率 vs 実的中率
| bt | n | 予測avg | 実的中率 | 校正誤差 | 過信度 | Brier |
|---|---|---|---|---|---|---|
| win | 413 | 0.4708 | 0.3196 | +0.1512 | 🟡+32% | 0.2377 |

### 戦略別: 校正精度 + Brier Skill Score
| sid | bt | n | pred | actual | Brier | BSS | ROI |
|---|---|---|---|---|---|---|---|
| S00 | win | 176 | 0.4323 | 0.2841 | 0.2311 | 🔴-0.14 | 0.746 |
| S01_NAKAANA1 | win | 162 | 0.4789 | 0.2840 | 0.2381 | 🔴-0.17 | 0.783 |
| S02_TETSUBAN | win | 75 | 0.5436 | 0.4800 | 0.2525 | 🔴-0.01 | 0.953 |

### 確率デシル別: 校正カーブ
| 確率帯 | n | 予測avg | 実的中率 | gap |
|---|---|---|---|---|
| 0.10-0.15 | 5 | 0.1313 | 0.2000 | 🔴-0.0687 |
| 0.15-0.20 | 6 | 0.1804 | 0.5000 | 🔴-0.3196 |
| 0.20-0.30 | 12 | 0.2272 | 0.3333 | 🔴-0.1061 |
| 0.30-0.50 | 162 | 0.4171 | 0.2778 | 🔴+0.1393 |
| 0.50+ | 225 | 0.5429 | 0.3511 | 🔴+0.1918 |

## Settlement Ratio データ品質

- 学習済み: 4バンド / fallback: 13バンド
| bt | odds帯 | source | n | ratio |
|---|---|---|---|---|
| win | <3.0 | ✅learned | 82 | 0.81 |
| win | <5.0 | ✅learned | 151 | 0.724 |
| win | <10.0 | ✅learned | 78 | 0.458 |
| win | <20.0 | ✅learned | 25 | 0.218 |
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
_auto-generated by claude_snapshot.py at 2026-07-23T16:30:01.375054+09:00_