# ClaudeDebug スナップショット

## 🔴 現状: RED

**生成**: 2026-11-03T12:20:02.093871+09:00

### 次に取るべきアクション
> RED最優先: CALIBRATION_DRIFT×28 (24h) → ログ/DB確認

### 検出された問題
- 🟡 FINAL_MISSING×120 (24h)
- 🔴 CALIBRATION_DRIFT×28 (24h)
- 🔴 CIRCUIT_BREAKER_TRIP×25 (24h)
- 🔴 STRATEGY_CI_FAIL×16 (24h)
- 🔴 alert_manager dispatch 失敗確定 1件（手動確認必要）

---

## 🔧 AI デバッグキュー（このClaudeが対処）

### 🟡 ANOMALY_SCRAPER_FAILURE_BURST  ×10  [2026-11-03T11:30:45]
- key: `ANOMALY_SCRAPER_FAILURE_BURST|`
- **FIX**: 直近1h でscraper 3-retry 全敗多発。boatrace.jp 側timeout / IP ban / DDoS

### 🔴 CALIBRATION_DRIFT  ×22  [2026-11-03T11:18:35]
- key: `CALIBRATION_DRIFT|`
- **FIX**: 予測確率が実的中率から50%以上乖離→isotonic_calibration.json 再生成 or モデル再学習が必要。EV計算が膨張中

### 🔴 CIRCUIT_BREAKER_TRIP  ×34  [2026-11-03T11:18:35]
- key: `CIRCUIT_BREAKER_TRIP|`
- **FIX**: 7日ROI<0.7→戦略を enabled:false にして原因調査。校正ドリフトか市場変化を確認

### 🔴 CIRCUIT_BREAKER_NO_ACTION  ×44  [2026-11-03T11:18:35]
- key: `CIRCUIT_BREAKER_NO_ACTION|`
- **FIX**: CIRCUIT_BREAKER_TRIP 発動済なのに strategies.json で enabled のまま。enabled:false に切替 or 復旧条件満たしたか確認

### 🔴 STRATEGY_CI_FAIL  ×22  [2026-11-03T11:18:35]
- key: `STRATEGY_CI_FAIL|`
- **FIX**: grid戦略のOOS CI下限<1.0→論文基準で赤字リスク。strategies.json確認

### 🔴 CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION  ×3  [2026-11-03T11:00:03]
- key: `CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION|戦略 S00 が TRIP してるが enabled のまま`
- **FIX**: CIRCUIT_BREAKER_TRIP 戦略が enabled のまま。enabled:false に

### 🔴 CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION  ×3  [2026-11-03T11:00:03]
- key: `CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION|戦略 S01_NAKAANA1 が TRIP してるが enabled のまま`
- **FIX**: CIRCUIT_BREAKER_TRIP 戦略が enabled のまま。enabled:false に

### 🟡 CODE_AUDIT_SCRAPER_FAILURE_RATE_HIGH  ×2  [2026-11-03T10:30:03]
- key: `CODE_AUDIT_SCRAPER_FAILURE_RATE_HIGH|直近 500 log行 で 3-retry 全敗 6 件 (閾値 3)`
- **FIX**: scraper 3-retry 全敗多発。boatrace.jp timeout or IP ban 疑い

### 🟡 ANOMALY_BET_VOLUME_DROP  ×22  [2026-11-03T10:01:11]
- key: `ANOMALY_BET_VOLUME_DROP|`
- **FIX**: 本日のbet数が7日baselineから2σ低下。戦略filter/ scan fix/run_cycle停止を疑え

### 🟡 CODE_AUDIT_SCRAPER_FAILURE_RATE_HIGH  ×1  [2026-11-03T09:30:03]
- key: `CODE_AUDIT_SCRAPER_FAILURE_RATE_HIGH|直近 500 log行 で 3-retry 全敗 8 件 (閾値 3)`
- **FIX**: scraper 3-retry 全敗多発。boatrace.jp timeout or IP ban 疑い

### 🟡 CODE_AUDIT_SCRAPER_FAILURE_RATE_HIGH  ×2  [2026-11-03T09:00:05]
- key: `CODE_AUDIT_SCRAPER_FAILURE_RATE_HIGH|直近 500 log行 で 3-retry 全敗 5 件 (閾値 3)`
- **FIX**: scraper 3-retry 全敗多発。boatrace.jp timeout or IP ban 疑い

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-11-03T06:00:13]
- key: `INSUFFICIENT_SAMPLE|S00: n=169<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### 🟡 ORPHAN_SCAN  ×1  [2026-11-03T06:00:13]
- key: `ORPHAN_SCAN|172 件の scan に final/retreat 追従無し`
- **FIX**: scan 後 final も retreat も無い→当該レースの final 窓が短すぎ/fetch 失敗

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-11-03T06:00:13]
- key: `INSUFFICIENT_SAMPLE|S02_TETSUBAN: n=63<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-11-03T06:00:13]
- key: `INSUFFICIENT_SAMPLE|S01_NAKAANA1: n=173<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ CALIBRATION_LIVE  ×1  [2026-11-03T06:00:13]
- key: `CALIBRATION_LIVE|decile 0.15-0.20: n=9 pred=0.1865 actual=0.0000 gap=+0.1865`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ DRIFT_BUCKET  ×1  [2026-11-03T06:00:13]
- key: `DRIFT_BUCKET|drift ≤-30%: n=22 hit%=50.0% ROI=1.35 (コスト 6,400/回収 8,660)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ ROI_STAT  ×1  [2026-11-03T06:00:13]
- key: `ROI_STAT|S00: n=169 hit%=29.6% hit_CI[Bonf]=[20.6,40.5]% ROI=0.78 ROI_boot95=[0.58,1.01]`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-11-03T06:00:13]
- key: `ROI_STAT|S01_NAKAANA1: n=173 hit%=32.9% hit_CI[Bonf]=[23.6,43.8]% ROI=0.81 ROI_boot95=[0.`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-11-03T06:00:13]
- key: `ROI_STAT|S02_TETSUBAN: n=63 hit%=47.6% hit_CI[Bonf]=[30.8,65.0]% ROI=1.08 ROI_boot95=[0.6`
- **FIX**: 統計サマリ情報。判定ではなく参照用


以下、詳細セクション（通常読み飛ばし可）

## 環境・コード状態
- git_sha: `<error: Command '['git', '-C', '/opt/boa` dirty=True
- config.json md5: `eb532e851a30cd2f7e69bdf0dfca3f2b`
- strategies.json md5: `06b22dd935785e7947bf9c0f170b69a3`
- numpy=2.4.4 lightgbm=4.6.0 scipy=1.17.1
- **calibration_applied**: True ← predictor.py が校正を呼んでるか
- DB: 17.51MB / last modified 2026-11-03T12:16:44.190485+09:00

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
trace.jp/owpc/pc/race/odds3t?rno=4&jcd=22&hd=20261103: HTTPSConnectionPool(host='www.boatrace.jp', port=443): Read timed out. (read timeout=10), retry in 3s
2026-11-03 12:18:22,820 [WARNING] scraper: fetch error (3/3): https://www.boatrace.jp/owpc/pc/race/odds3t?rno=4&jcd=22&hd=20261103: HTTPSConnectionPool(host='www.boatrace.jp', port=443): Read timed out. (read timeout=10), retry in 9s
2026-11-03 12:18:22,821 [ERROR] scraper: fetch failed after 3 retries: https://www.boatrace.jp/owpc/pc/race/odds3t?rno=4&jcd=22&hd=20261103
2026-11-03 12:18:31,946 [INFO] scraper: odds3f: 20/20 parsed
2026-11-03 12:18:42,959 [WARNING] scraper: fetch error (1/3): https://www.boatrace.jp/owpc/pc/race/odds2tf?rno=4&jcd=22&hd=20261103: HTTPSConnectionPool(host='www.boatrace.jp', port=443): Read timed out. (read timeout=10), retry in 1s
2026-11-03 12:18:53,169 [INFO] scraper: odds2t: 30/30 parsed
2026-11-03 12:18:53,170 [INFO] scraper: odds2f: 15/15 parsed
2026-11-03 12:19:04,182 [WARNING] scraper: fetch error (1/3): https://www.boatrace.jp/owpc/pc/race/oddstf?rno=4&jcd=22&hd=20261103: HTTPSConnectionPool(host='www.boatrace.jp', port=443): Read timed out. (read timeout=10), retry in 1s
2026-11-03 12:19:15,223 [WARNING] scraper: fetch error (2/3): https://www.boatrace.jp/owpc/pc/race/oddstf?rno=4&jcd=22&hd=20261103: HTTPSConnectionPool(host='www.boatrace.jp', port=443): Read timed out. (read timeout=10), retry in 3s
2026-11-03 12:19:27,354 [INFO] scraper: odds_win: 6/6 parsed
2026-11-03 12:19:27,354 [INFO] scraper: fetch_race 22/4: boats=6 odds=71/191
2026-11-03 12:19:27,356 [INFO] predictor: CALIBRATION_MODE=on
2026-11-03 12:19:27,356 [INFO] predictor: combos: {'win': 6, '2t': 30}
2026-11-03 12:19:27,357 [INFO] run_cycle: fetched 22/4 [final]: 36 combos
2026-11-03 12:19:47,634 [WARNING] scraper: fetch error (1/3): https://www.boatrace.jp/owpc/pc/race/beforeinfo?rno=5&jcd=09&hd=20261103: HTTPSConnectionPool(host='www.boatrace.jp', port=443): Read timed out. (read timeout=10), retry in 1s

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
    "c": 31
  },
  {
    "target": "primary",
    "ok": 1,
    "c": 31
  }
]
```

## Phase別通知記録 (24h)
{'final': 10, 'result': 5, 'scan': 16}

## アラート件数 (24h・種類別)
```
  ANOMALY_SCRAPER_FAILURE_BURST: 308
  FINAL_MISSING: 120
  CALIBRATION_DRIFT: 28
  CIRCUIT_BREAKER_TRIP: 25
  ANOMALY_SCAN_FINAL_RATIO: 21
  CIRCUIT_BREAKER_NO_ACTION: 19
  STRATEGY_CI_FAIL: 16
  ANOMALY_BET_VOLUME_DROP: 1
```

## 戦略別 ROI (7日)
| sid | n | hits | cost | payout | PL | ROI |
|---|---|---|---|---|---|---|
| S00 | 24 | 4 | 7,200 | 3,180 | -4,020 | 0.442 |
| S01_NAKAANA1 | 25 | 7 | 5,000 | 3,880 | -1,120 | 0.776 |
| S02_TETSUBAN | 9 | 1 | 1,800 | 360 | -1,440 | 0.2 |

## 直近アラート (24h・新しい順)
```
[12:16:38] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 503}
[12:14:48] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 505}
[12:10:18] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 501}
[12:02:47] CIRCUIT_BREAKER_TRIP: {"cost": 7200, "kind": "CIRCUIT_BREAKER_TRIP", "n": 24, "payout": 3180, "roi_7d": 0.442, "sid": "S00"}
[12:02:47] CALIBRATION_DRIFT: {"avg_actual": 0.2143, "avg_pred": 0.4746, "bt": "win", "kind": "CALIBRATION_DRIFT", "n": 56, "overconf_pct": 54.8}
[11:59:10] CIRCUIT_BREAKER_NO_ACTION: {"kind": "CIRCUIT_BREAKER_NO_ACTION", "sid": "S01_NAKAANA1"}
[11:55:39] CALIBRATION_DRIFT: {"avg_actual": 0.2105, "avg_pred": 0.4735, "bt": "win", "kind": "CALIBRATION_DRIFT", "n": 57, "overconf_pct": 55.5}
[11:53:26] CALIBRATION_DRIFT: {"avg_actual": 0.2069, "avg_pred": 0.4738, "bt": "win", "kind": "CALIBRATION_DRIFT", "n": 58, "overconf_pct": 56.3}
[11:51:41] CIRCUIT_BREAKER_TRIP: {"cost": 4800, "kind": "CIRCUIT_BREAKER_TRIP", "n": 24, "payout": 3100, "roi_7d": 0.646, "sid": "S01_NAKAANA1"}
[11:51:41] CIRCUIT_BREAKER_TRIP: {"cost": 7500, "kind": "CIRCUIT_BREAKER_TRIP", "n": 25, "payout": 3180, "roi_7d": 0.424, "sid": "S00"}
```

## 本日残レース: 91件

## 本日nidレジャー（ID単位完遂突合せ）
- race_schedule: 132件 登録 / 41件 締切済
- 通知発射: scan=5 nid / final=4 nid / result=1 nid
- predictions: 3 / うち結果DB記録済: 1
- ✅ 結果DBあるが通知未発射: 0件 `tools/backfill_result_notifications.py` で救済可
- 🔴 scan後final無しのまま締切: 4件（FINAL_MISSING の温床）

## 直近送信失敗 (24h)
```
```

## 最新 predictions サンプル (計算spot-check用)
| sid | race | bt | combo | p | odds | ev | bet | at |
|---|---|---|---|---|---|---|---|---|
| S01_NAKAANA1 | 175R | win | 1 | 0.4111 | 3.9 | 1.60 | 200 | scan=- drift=- | 12:12:01 |
| S01_NAKAANA1 | 043R | win | 1 | 0.3177 | 4.8 | 1.53 | 200 | scan=- drift=- | 11:48:48 |
| S01_NAKAANA1 | 042R | win | 1 | 0.4989 | 3.9 | 1.95 | 200 | scan=4.1 drift=-4.9% | 11:21:03 |
| S02_TETSUBAN | 0310R | win | 1 | 0.5334 | 2.1 | 1.12 | 200 | scan=- drift=- | 14:58:13 |
| S01_NAKAANA1 | 097R | win | 1 | 0.5990 | 3.2 | 1.92 | 200 | scan=3.2 drift=+0.0% | 13:21:36 |
| S02_TETSUBAN | 036R | win | 1 | 0.5719 | 2.2 | 1.26 | 200 | scan=- drift=- | 13:08:13 |
| S01_NAKAANA1 | 043R | win | 1 | 0.4111 | 4.6 | 1.89 | 200 | scan=- drift=- | 11:47:38 |
| S02_TETSUBAN | 0711R | win | 1 | 0.4989 | 2.6 | 1.30 | 200 | scan=2.3 drift=+13.0% | 20:05:24 |
| S00 | 1810R | win | 1 | 0.4111 | 15.0 | 6.17 | 300 | scan=12.0 drift=+25.0% | 13:06:12 |
| S00 | 224R | win | 1 | 0.4111 | 16.5 | 6.78 | 300 | scan=- drift=- | 12:13:13 |

## オッズドリフト統計 (7日)

| bt | n | avg | min | max | down10 | collapse(≤-30%) | any_large(≥10%) |
|---|---|---|---|---|---|---|---|
| win | 32 | +3.8% | -54.4% | +77.7% | 8 | 5 | 20 |

## 校正テーブル合格状況

- total: 27 グループ
- passed: 19
- failed: 8 — `2f|4, 2f|5, 3f|2, 3f|3, 3f|4, 3t|1, 3t|4, 3t|5`
- 主力グループ状態: ✅ (全12グループ合格)

## SRE Golden Signals (24h)

| Signal | Value |
|---|---|
| **Latency** (scan→final avg) | 411.3s |
| **Latency** (scan→final max) | 609.8s |
| **Traffic** (notifications 24h) | 31 |
| **Errors** (send fail rate) | ✅ 0.0% |
| **Saturation** (S01_NAKAANA1) | 600円 used |

## 信ぴょう性メトリクス（予測精度の証拠）

### bt別: 予測確率 vs 実的中率
| bt | n | 予測avg | 実的中率 | 校正誤差 | 過信度 | Brier |
|---|---|---|---|---|---|---|
| win | 396 | 0.4783 | 0.3434 | +0.1349 | 🟡+28% | 0.2368 |

### 戦略別: 校正精度 + Brier Skill Score
| sid | bt | n | pred | actual | Brier | BSS | ROI |
|---|---|---|---|---|---|---|---|
| S00 | win | 165 | 0.4400 | 0.3030 | 0.2240 | 🔴-0.06 | 0.795 |
| S01_NAKAANA1 | win | 168 | 0.4878 | 0.3333 | 0.2392 | 🔴-0.08 | 0.813 |
| S02_TETSUBAN | win | 63 | 0.5532 | 0.4762 | 0.2641 | 🔴-0.06 | 1.081 |

### 確率デシル別: 校正カーブ
| 確率帯 | n | 予測avg | 実的中率 | gap |
|---|---|---|---|---|
| 0.15-0.20 | 8 | 0.1878 | 0.0000 | 🔴+0.1878 |
| 0.20-0.30 | 9 | 0.2290 | 0.1111 | 🔴+0.1179 |
| 0.30-0.50 | 140 | 0.4094 | 0.3071 | 🔴+0.1022 |
| 0.50+ | 235 | 0.5450 | 0.3872 | 🔴+0.1577 |

## Settlement Ratio データ品質

- 学習済み: 4バンド / fallback: 13バンド
| bt | odds帯 | source | n | ratio |
|---|---|---|---|---|
| win | <3.0 | ✅learned | 197 | 0.811 |
| win | <5.0 | ✅learned | 361 | 0.742 |
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
_auto-generated by claude_snapshot.py at 2026-11-03T12:20:02.093871+09:00_