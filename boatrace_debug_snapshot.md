# ClaudeDebug スナップショット

## 🔴 現状: RED

**生成**: 2026-11-04T11:50:01.203030+09:00

### 次に取るべきアクション
> RED最優先: CALIBRATION_DRIFT×36 (24h) → ログ/DB確認

### 検出された問題
- 🟡 FINAL_MISSING×57 (24h)
- 🔴 CALIBRATION_DRIFT×36 (24h)
- 🔴 CIRCUIT_BREAKER_TRIP×20 (24h)
- 🔴 STRATEGY_CI_FAIL×17 (24h)
- 🔴 PSI_DRIFT_DETECTED×3 (24h)
- 🟡 LARGE_ODDS_DRIFT×1 (24h)
- 🔴 alert_manager dispatch 失敗確定 1件（手動確認必要）

---

## 🔧 AI デバッグキュー（このClaudeが対処）

### 🟡 CODE_AUDIT_SCRAPER_FAILURE_RATE_HIGH  ×1  [2026-11-04T11:30:06]
- key: `CODE_AUDIT_SCRAPER_FAILURE_RATE_HIGH|直近 500 log行 で 3-retry 全敗 11 件 (閾値 3)`
- **FIX**: scraper 3-retry 全敗多発。boatrace.jp timeout or IP ban 疑い

### 🟡 ANOMALY_SCRAPER_FAILURE_BURST  ×9  [2026-11-04T11:22:15]
- key: `ANOMALY_SCRAPER_FAILURE_BURST|`
- **FIX**: 直近1h でscraper 3-retry 全敗多発。boatrace.jp 側timeout / IP ban / DDoS

### 🔴 CALIBRATION_DRIFT  ×13  [2026-11-04T11:07:28]
- key: `CALIBRATION_DRIFT|`
- **FIX**: 予測確率が実的中率から50%以上乖離→isotonic_calibration.json 再生成 or モデル再学習が必要。EV計算が膨張中

### 🔴 CIRCUIT_BREAKER_NO_ACTION  ×26  [2026-11-04T11:07:28]
- key: `CIRCUIT_BREAKER_NO_ACTION|`
- **FIX**: CIRCUIT_BREAKER_TRIP 発動済なのに strategies.json で enabled のまま。enabled:false に切替 or 復旧条件満たしたか確認

### 🔴 STRATEGY_CI_FAIL  ×13  [2026-11-04T11:07:28]
- key: `STRATEGY_CI_FAIL|`
- **FIX**: grid戦略のOOS CI下限<1.0→論文基準で赤字リスク。strategies.json確認

### 🔴 PSI_DRIFT_DETECTED  ×3  [2026-11-04T11:02:14]
- key: `PSI_DRIFT_DETECTED|`
- **FIX**: ml_prob 分布の PSI>0.25→モデル入力の分布シフト。校正テーブル再生成 or モデル再学習を検討

### 🟡 CODE_AUDIT_SCRAPER_FAILURE_RATE_HIGH  ×1  [2026-11-04T11:00:03]
- key: `CODE_AUDIT_SCRAPER_FAILURE_RATE_HIGH|直近 500 log行 で 3-retry 全敗 7 件 (閾値 3)`
- **FIX**: scraper 3-retry 全敗多発。boatrace.jp timeout or IP ban 疑い

### 🔴 CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION  ×3  [2026-11-04T10:30:08]
- key: `CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION|戦略 S00 が TRIP してるが enabled のまま`
- **FIX**: CIRCUIT_BREAKER_TRIP 戦略が enabled のまま。enabled:false に

### 🔴 CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION  ×3  [2026-11-04T10:30:08]
- key: `CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION|戦略 S01_NAKAANA1 が TRIP してるが enabled のまま`
- **FIX**: CIRCUIT_BREAKER_TRIP 戦略が enabled のまま。enabled:false に

### 🟡 CODE_AUDIT_SCRAPER_FAILURE_RATE_HIGH  ×2  [2026-11-04T10:00:03]
- key: `CODE_AUDIT_SCRAPER_FAILURE_RATE_HIGH|直近 500 log行 で 3-retry 全敗 4 件 (閾値 3)`
- **FIX**: scraper 3-retry 全敗多発。boatrace.jp timeout or IP ban 疑い

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-11-04T06:00:12]
- key: `INSUFFICIENT_SAMPLE|S02_TETSUBAN: n=62<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-11-04T06:00:12]
- key: `INSUFFICIENT_SAMPLE|S00: n=161<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-11-04T06:00:12]
- key: `INSUFFICIENT_SAMPLE|S01_NAKAANA1: n=166<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### 🟡 ORPHAN_SCAN  ×1  [2026-11-04T06:00:12]
- key: `ORPHAN_SCAN|174 件の scan に final/retreat 追従無し`
- **FIX**: scan 後 final も retreat も無い→当該レースの final 窓が短すぎ/fetch 失敗

### ℹ️ CALIBRATION_LIVE  ×1  [2026-11-04T06:00:12]
- key: `CALIBRATION_LIVE|decile 0.20-0.30: n=9 pred=0.2290 actual=0.1111 gap=+0.1179`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-11-04T06:00:12]
- key: `ROI_STAT|S00: n=161 hit%=30.4% hit_CI[Bonf]=[21.1,41.7]% ROI=0.80 ROI_boot95=[0.58,1.04]`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-11-04T06:00:12]
- key: `ROI_STAT|S01_NAKAANA1: n=166 hit%=33.1% hit_CI[Bonf]=[23.6,44.3]% ROI=0.79 ROI_boot95=[0.`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-11-04T06:00:12]
- key: `ROI_STAT|S02_TETSUBAN: n=62 hit%=46.8% hit_CI[Bonf]=[30.0,64.3]% ROI=1.08 ROI_boot95=[0.6`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ DRIFT_BUCKET  ×1  [2026-11-04T06:00:12]
- key: `DRIFT_BUCKET|drift ≤-30%: n=21 hit%=47.6% ROI=1.26 (コスト 6,200/回収 7,800)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-11-04T06:00:12]
- key: `DRIFT_BUCKET|drift -30%〜-10%: n=36 hit%=36.1% ROI=0.99 (コスト 8,300/回収 8,250)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料


以下、詳細セクション（通常読み飛ばし可）

## 環境・コード状態
- git_sha: `<error: Command '['git', '-C', '/opt/boa` dirty=True
- config.json md5: `eb532e851a30cd2f7e69bdf0dfca3f2b`
- strategies.json md5: `06b22dd935785e7947bf9c0f170b69a3`
- numpy=2.4.4 lightgbm=4.6.0 scipy=1.17.1
- **calibration_applied**: True ← predictor.py が校正を呼んでるか
- DB: 17.54MB / last modified 2026-11-04T11:49:56.552431+09:00

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
race.jp', port=443): Read timed out. (read timeout=10), retry in 3s
2026-11-04 11:48:27,364 [WARNING] scraper: fetch error (3/3): https://www.boatrace.jp/owpc/pc/race/odds2tf?rno=4&jcd=06&hd=20261104: HTTPSConnectionPool(host='www.boatrace.jp', port=443): Read timed out. (read timeout=10), retry in 9s
2026-11-04 11:48:27,365 [ERROR] scraper: fetch failed after 3 retries: https://www.boatrace.jp/owpc/pc/race/odds2tf?rno=4&jcd=06&hd=20261104
2026-11-04 11:48:36,751 [INFO] scraper: odds_win: 3/6 parsed
2026-11-04 11:48:36,751 [INFO] scraper: fetch_race 06/4: boats=6 odds=143/191
2026-11-04 11:48:36,754 [INFO] predictor: CALIBRATION_MODE=on
2026-11-04 11:48:36,754 [INFO] predictor: combos: {'win': 3, '3t': 120}
2026-11-04 11:48:36,757 [INFO] run_cycle: fetched 06/4 [scan]: 123 combos
2026-11-04 11:49:08,210 [WARNING] scraper: fetch error (1/3): https://www.boatrace.jp/owpc/pc/race/odds3t?rno=8&jcd=21&hd=20261104: HTTPSConnectionPool(host='www.boatrace.jp', port=443): Read timed out. (read timeout=10), retry in 1s
2026-11-04 11:49:17,380 [INFO] scraper: odds3t: 120/120 parsed
2026-11-04 11:49:26,460 [INFO] scraper: odds3f: 20/20 parsed
2026-11-04 11:49:35,568 [INFO] scraper: odds2t: 30/30 parsed
2026-11-04 11:49:35,569 [INFO] scraper: odds2f: 15/15 parsed
2026-11-04 11:49:44,672 [INFO] scraper: odds_win: 3/6 parsed
2026-11-04 11:49:44,672 [INFO] scraper: fetch_race 21/8: boats=6 odds=188/191
2026-11-04 11:49:44,675 [INFO] predictor: CALIBRATION_MODE=on
2026-11-04 11:49:44,675 [INFO] predictor: combos: {'win': 3, '2t': 30, '3t': 120}
2026-11-04 11:49:44,678 [INFO] run_cycle: fetched 21/8 [scan]: 153 combos
2026-11-04 11:49:49,797 [INFO] race_id: notif: nid=2026110421081159 sid=S00 phase=scan rank=SS
2026-11-04 11:49:50,274 [INFO] notifier: Discord notify OK (status=204)
2026-11-04 11:49:55,573 [INFO] notifier: Discord notify OK (status=204)
2026-11-04 11:49:55,615 [INFO] run_cycle: SCAN S00 芦屋8R SS
2026-11-04 11:49:55,717 [INFO] run_cycle: run_cycle done: 1 notifications

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
    "c": 28
  },
  {
    "target": "primary",
    "ok": 1,
    "c": 28
  }
]
```

## Phase別通知記録 (24h)
{'final': 9, 'result': 8, 'scan': 11}

## アラート件数 (24h・種類別)
```
  ANOMALY_SCRAPER_FAILURE_BURST: 242
  FINAL_MISSING: 57
  CALIBRATION_DRIFT: 36
  CIRCUIT_BREAKER_NO_ACTION: 34
  CIRCUIT_BREAKER_TRIP: 20
  STRATEGY_CI_FAIL: 17
  PSI_DRIFT_DETECTED: 3
  LARGE_ODDS_DRIFT: 1
```

## 戦略別 ROI (7日)
| sid | n | hits | cost | payout | PL | ROI |
|---|---|---|---|---|---|---|
| S00 | 19 | 3 | 5,700 | 2,610 | -3,090 | 0.458 |
| S01_NAKAANA1 | 20 | 6 | 4,000 | 3,140 | -860 | 0.785 |
| S02_TETSUBAN | 8 | 0 | 1,600 | 0 | -1,600 | 0.0 |

## 直近アラート (24h・新しい順)
```
[11:49:55] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 12, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 510}
[11:46:49] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 11, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 499}
[11:42:22] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 11, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 496}
[11:38:03] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 10, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 498}
[11:36:39] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 10, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 490}
[11:34:50] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 9, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 489}
[11:31:17] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 11, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 488}
[11:29:14] CALIBRATION_DRIFT: {"avg_actual": 0.1915, "avg_pred": 0.4732, "bt": "win", "kind": "CALIBRATION_DRIFT", "n": 47, "overconf_pct": 59.5}
[11:29:14] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 11, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 489}
[11:22:13] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 8, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 486}
```

## 本日残レース: 111件

## 本日nidレジャー（ID単位完遂突合せ）
- race_schedule: 144件 登録 / 33件 締切済
- 通知発射: scan=6 nid / final=5 nid / result=2 nid
- predictions: 2 / うち結果DB記録済: 2
- ✅ 結果DBあるが通知未発射: 0件 `tools/backfill_result_notifications.py` で救済可
- 🔴 scan後final無しのまま締切: 2件（FINAL_MISSING の温床）

## 直近送信失敗 (24h)
```
```

## 最新 predictions サンプル (計算spot-check用)
| sid | race | bt | combo | p | odds | ev | bet | at |
|---|---|---|---|---|---|---|---|---|
| S02_TETSUBAN | 092R | win | 1 | 0.5123 | 2.0 | 1.02 | 200 | scan=- drift=- | 10:55:26 |
| S02_TETSUBAN | 212R | win | 1 | 0.5735 | 2.4 | 1.38 | 200 | scan=- drift=- | 08:59:15 |
| S01_NAKAANA1 | 191R | win | 1 | 0.4989 | 3.1 | 1.55 | 200 | scan=3.5 drift=-11.4% | 17:40:03 |
| S01_NAKAANA1 | 154R | win | 1 | 0.4989 | 3.5 | 1.75 | 200 | scan=4.3 drift=-18.6% | 16:41:26 |
| S01_NAKAANA1 | 1011R | win | 1 | 0.4989 | 3.0 | 1.50 | 200 | scan=3.0 drift=+0.0% | 13:48:39 |
| S01_NAKAANA1 | 175R | win | 1 | 0.4111 | 3.9 | 1.60 | 200 | scan=- drift=- | 12:12:01 |
| S01_NAKAANA1 | 043R | win | 1 | 0.3177 | 4.8 | 1.53 | 200 | scan=- drift=- | 11:48:48 |
| S01_NAKAANA1 | 042R | win | 1 | 0.4989 | 3.9 | 1.95 | 200 | scan=4.1 drift=-4.9% | 11:21:03 |
| S02_TETSUBAN | 0310R | win | 1 | 0.5334 | 2.1 | 1.12 | 200 | scan=- drift=- | 14:58:13 |
| S01_NAKAANA1 | 097R | win | 1 | 0.5990 | 3.2 | 1.92 | 200 | scan=3.2 drift=+0.0% | 13:21:36 |

## オッズドリフト統計 (7日)

| bt | n | avg | min | max | down10 | collapse(≤-30%) | any_large(≥10%) |
|---|---|---|---|---|---|---|---|
| win | 24 | -0.1% | -54.4% | +66.7% | 6 | 4 | 13 |

## 校正テーブル合格状況

- total: 27 グループ
- passed: 19
- failed: 8 — `2f|4, 2f|5, 3f|2, 3f|3, 3f|4, 3t|1, 3t|4, 3t|5`
- 主力グループ状態: ✅ (全12グループ合格)

## SRE Golden Signals (24h)

| Signal | Value |
|---|---|
| **Latency** (scan→final avg) | 405.7s |
| **Latency** (scan→final max) | 584.2s |
| **Traffic** (notifications 24h) | 28 |
| **Errors** (send fail rate) | ✅ 0.0% |
| **Saturation** (S02_TETSUBAN) | 400円 used |

## 信ぴょう性メトリクス（予測精度の証拠）

### bt別: 予測確率 vs 実的中率
| bt | n | 予測avg | 実的中率 | 校正誤差 | 過信度 | Brier |
|---|---|---|---|---|---|---|
| win | 388 | 0.4783 | 0.3351 | +0.1433 | 🟡+30% | 0.2358 |

### 戦略別: 校正精度 + Brier Skill Score
| sid | bt | n | pred | actual | Brier | BSS | ROI |
|---|---|---|---|---|---|---|---|
| S00 | win | 160 | 0.4394 | 0.3000 | 0.2235 | 🔴-0.06 | 0.799 |
| S01_NAKAANA1 | win | 164 | 0.4871 | 0.3232 | 0.2361 | 🔴-0.08 | 0.762 |
| S02_TETSUBAN | win | 64 | 0.5532 | 0.4531 | 0.2658 | 🔴-0.07 | 1.048 |

### 確率デシル別: 校正カーブ
| 確率帯 | n | 予測avg | 実的中率 | gap |
|---|---|---|---|---|
| 0.15-0.20 | 8 | 0.1878 | 0.0000 | 🔴+0.1878 |
| 0.20-0.30 | 9 | 0.2290 | 0.1111 | 🔴+0.1179 |
| 0.30-0.50 | 138 | 0.4113 | 0.2971 | 🔴+0.1142 |
| 0.50+ | 229 | 0.5450 | 0.3799 | 🔴+0.1651 |

## Settlement Ratio データ品質

- 学習済み: 4バンド / fallback: 13バンド
| bt | odds帯 | source | n | ratio |
|---|---|---|---|---|
| win | <3.0 | ✅learned | 197 | 0.811 |
| win | <5.0 | ✅learned | 363 | 0.741 |
| win | <10.0 | ✅learned | 157 | 0.451 |
| win | <20.0 | ✅learned | 47 | 0.249 |
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
_auto-generated by claude_snapshot.py at 2026-11-04T11:50:01.203030+09:00_