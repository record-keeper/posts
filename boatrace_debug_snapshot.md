# ClaudeDebug スナップショット

## 🔴 現状: RED

**生成**: 2026-07-23T11:00:01.945158+09:00

### 次に取るべきアクション
> RED最優先: CIRCUIT_BREAKER_TRIP×46 (24h) → ログ/DB確認

### 検出された問題
- 🔴 CIRCUIT_BREAKER_TRIP×46 (24h)
- 🟡 FINAL_MISSING×43 (24h)
- 🔴 STRATEGY_CI_FAIL×17 (24h)
- 🔴 CALIBRATION_DRIFT×7 (24h)
- 🟡 LARGE_ODDS_DRIFT×1 (24h)
- 🔴 alert_manager dispatch 失敗確定 1件（手動確認必要）

---

## 🔧 AI デバッグキュー（このClaudeが対処）

### 🔴 CALIBRATION_DRIFT  ×3  [2026-07-23T10:57:27]
- key: `CALIBRATION_DRIFT|`
- **FIX**: 予測確率が実的中率から50%以上乖離→isotonic_calibration.json 再生成 or モデル再学習が必要。EV計算が膨張中

### 🟡 ANOMALY_SCAN_FINAL_RATIO  ×25  [2026-07-23T10:35:28]
- key: `ANOMALY_SCAN_FINAL_RATIO|`
- **FIX**: scan→final成立率が7日baselineから2σ逸脱。scan/final window設定・odds取得タイミング

### 🔴 CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION  ×2  [2026-07-23T10:30:03]
- key: `CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION|戦略 S00 が TRIP してるが enabled のまま`
- **FIX**: CIRCUIT_BREAKER_TRIP 戦略が enabled のまま。enabled:false に

### 🔴 CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION  ×2  [2026-07-23T10:30:03]
- key: `CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION|戦略 S01_NAKAANA1 が TRIP してるが enabled のまま`
- **FIX**: CIRCUIT_BREAKER_TRIP 戦略が enabled のまま。enabled:false に

### 🟡 ANOMALY_SCRAPER_FAILURE_BURST  ×31  [2026-07-23T10:29:39]
- key: `ANOMALY_SCRAPER_FAILURE_BURST|`
- **FIX**: 直近1h でscraper 3-retry 全敗多発。boatrace.jp 側timeout / IP ban / DDoS

### 🔴 CIRCUIT_BREAKER_TRIP  ×118  [2026-07-23T10:01:30]
- key: `CIRCUIT_BREAKER_TRIP|`
- **FIX**: 7日ROI<0.7→戦略を enabled:false にして原因調査。校正ドリフトか市場変化を確認

### 🔴 CIRCUIT_BREAKER_NO_ACTION  ×118  [2026-07-23T10:01:30]
- key: `CIRCUIT_BREAKER_NO_ACTION|`
- **FIX**: CIRCUIT_BREAKER_TRIP 発動済なのに strategies.json で enabled のまま。enabled:false に切替 or 復旧条件満たしたか確認

### 🔴 STRATEGY_CI_FAIL  ×59  [2026-07-23T10:01:30]
- key: `STRATEGY_CI_FAIL|`
- **FIX**: grid戦略のOOS CI下限<1.0→論文基準で赤字リスク。strategies.json確認

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
- DB: 8.4MB / last modified 2026-07-23T11:00:04.214640+09:00

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
p/owpc/pc/race/racelist?rno=2&jcd=08&hd=20260723: HTTPSConnectionPool(host='www.boatrace.jp', port=443): Read timed out. (read timeout=10), retry in 1s
2026-07-23 10:58:26,279 [WARNING] scraper: fetch error (2/3): https://www.boatrace.jp/owpc/pc/race/racelist?rno=2&jcd=08&hd=20260723: HTTPSConnectionPool(host='www.boatrace.jp', port=443): Read timed out. (read timeout=10), retry in 3s
2026-07-23 10:58:39,337 [WARNING] scraper: fetch error (3/3): https://www.boatrace.jp/owpc/pc/race/racelist?rno=2&jcd=08&hd=20260723: HTTPSConnectionPool(host='www.boatrace.jp', port=443): Read timed out. (read timeout=10), retry in 9s
2026-07-23 10:58:39,337 [ERROR] scraper: fetch failed after 3 retries: https://www.boatrace.jp/owpc/pc/race/racelist?rno=2&jcd=08&hd=20260723
2026-07-23 10:58:39,337 [ERROR] scraper: racelist fetch failed: jcd=08 rno=2
2026-07-23 10:58:39,337 [WARNING] run_cycle: fetch None: 08/2
2026-07-23 10:58:39,337 [INFO] run_cycle: run_cycle done: 0 notifications
2026-07-23 10:59:03,955 [INFO] run_cycle: === run_cycle 10:59:03 ===
2026-07-23 10:59:03,955 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-07-23 10:59:03,955 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-07-23 10:59:03,982 [INFO] predictor: Models loaded OK
2026-07-23 10:59:16,662 [INFO] scraper: odds3t: 120/120 parsed
2026-07-23 10:59:17,763 [INFO] scraper: odds3f: 20/20 parsed
2026-07-23 10:59:19,124 [INFO] scraper: odds2t: 29/30 parsed
2026-07-23 10:59:19,126 [INFO] scraper: odds2f: 15/15 parsed
2026-07-23 10:59:20,320 [INFO] scraper: odds_win: 3/6 parsed
2026-07-23 10:59:20,320 [INFO] scraper: fetch_race 08/2: boats=6 odds=187/191
2026-07-23 10:59:20,323 [INFO] predictor: CALIBRATION_MODE=on
2026-07-23 10:59:20,323 [INFO] predictor: combos: {'win': 3, '2t': 29, '3t': 120}
2026-07-23 10:59:20,327 [INFO] run_cycle: fetched 08/2 [scan]: 152 combos
2026-07-23 10:59:20,426 [INFO] run_cycle: run_cycle done: 0 notifications

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
    "c": 52
  },
  {
    "target": "primary",
    "ok": 1,
    "c": 52
  }
]
```

## Phase別通知記録 (24h)
{'final': 21, 'result': 11, 'scan': 20}

## アラート件数 (24h・種類別)
```
  ANOMALY_SCRAPER_FAILURE_BURST: 78
  CIRCUIT_BREAKER_TRIP: 46
  FINAL_MISSING: 43
  CIRCUIT_BREAKER_NO_ACTION: 34
  STRATEGY_CI_FAIL: 17
  CALIBRATION_DRIFT: 7
  ANOMALY_SCAN_FINAL_RATIO: 4
  LARGE_ODDS_DRIFT: 1
```

## 戦略別 ROI (7日)
| sid | n | hits | cost | payout | PL | ROI |
|---|---|---|---|---|---|---|
| S00 | 41 | 8 | 12,300 | 7,530 | -4,770 | 0.612 |
| S01_NAKAANA1 | 41 | 6 | 8,200 | 4,480 | -3,720 | 0.546 |
| S02_TETSUBAN | 17 | 9 | 3,400 | 3,500 | +100 | 1.029 |

## 直近アラート (24h・新しい順)
```
[10:59:20] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 5, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 818}
[10:58:39] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 5, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 809}
[10:57:26] CIRCUIT_BREAKER_TRIP: {"cost": 8200, "kind": "CIRCUIT_BREAKER_TRIP", "n": 41, "payout": 4480, "roi_7d": 0.546, "sid": "S01_NAKAANA1"}
[10:57:26] CALIBRATION_DRIFT: {"avg_actual": 0.2323, "avg_pred": 0.4678, "bt": "win", "kind": "CALIBRATION_DRIFT", "n": 99, "overconf_pct": 50.3}
[10:57:26] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 4, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 804}
[10:56:18] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 4, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 795}
[10:55:27] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 4, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 796}
[10:53:04] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 4, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 778}
[10:52:25] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 4, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 777}
[10:51:20] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 4, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 770}
```

## 本日残レース: 134件

## 本日nidレジャー（ID単位完遂突合せ）
- race_schedule: 156件 登録 / 22件 締切済
- 通知発射: scan=3 nid / final=2 nid / result=1 nid
- predictions: 1 / うち結果DB記録済: 1
- ✅ 結果DBあるが通知未発射: 0件 `tools/backfill_result_notifications.py` で救済可
- 🔴 scan後final無しのまま締切: 2件（FINAL_MISSING の温床）

## 直近送信失敗 (24h)
```
```

## 最新 predictions サンプル (計算spot-check用)
| sid | race | bt | combo | p | odds | ev | bet | at |
|---|---|---|---|---|---|---|---|---|
| S02_TETSUBAN | 213R | win | 1 | 0.5891 | 2.4 | 1.41 | 200 | scan=- drift=- | 09:21:18 |
| S01_NAKAANA1 | 246R | win | 1 | 0.5123 | 3.5 | 1.79 | 200 | scan=- drift=- | 19:53:18 |
| S00 | 154R | win | 1 | 0.5174 | 5.1 | 2.64 | 300 | scan=9.0 drift=-43.3% | 16:58:30 |
| S02_TETSUBAN | 058R | win | 1 | 0.5990 | 2.0 | 1.20 | 200 | scan=- drift=- | 15:02:30 |
| S01_NAKAANA1 | 054R | win | 1 | 0.4111 | 4.7 | 1.93 | 200 | scan=3.0 drift=+56.7% | 13:00:22 |
| S00 | 054R | win | 1 | 0.4111 | 4.7 | 1.93 | 300 | scan=6.3 drift=-25.4% | 13:00:20 |
| S02_TETSUBAN | 053R | win | 1 | 0.5735 | 2.1 | 1.20 | 200 | scan=- drift=- | 12:28:19 |
| S01_NAKAANA1 | 109R | win | 1 | 0.4989 | 3.3 | 1.65 | 200 | scan=- drift=- | 12:11:29 |
| S00 | 148R | win | 1 | 0.5719 | 4.3 | 2.46 | 300 | scan=- drift=- | 11:55:18 |
| S01_NAKAANA1 | 083R | win | 1 | 0.5735 | 3.5 | 2.01 | 200 | scan=- drift=- | 11:37:18 |

## オッズドリフト統計 (7日)

| bt | n | avg | min | max | down10 | collapse(≤-30%) | any_large(≥10%) |
|---|---|---|---|---|---|---|---|
| win | 48 | +23.4% | -83.7% | +628.9% | 19 | 8 | 37 |

## 校正テーブル合格状況

- total: 27 グループ
- passed: 19
- failed: 8 — `2f|4, 2f|5, 3f|2, 3f|3, 3f|4, 3t|1, 3t|4, 3t|5`
- 主力グループ状態: ✅ (全12グループ合格)

## SRE Golden Signals (24h)

| Signal | Value |
|---|---|
| **Latency** (scan→final avg) | 459.3s |
| **Latency** (scan→final max) | 618.2s |
| **Traffic** (notifications 24h) | 52 |
| **Errors** (send fail rate) | ✅ 0.0% |
| **Saturation** (S02_TETSUBAN) | 200円 used |

## 信ぴょう性メトリクス（予測精度の証拠）

### bt別: 予測確率 vs 実的中率
| bt | n | 予測avg | 実的中率 | 校正誤差 | 過信度 | Brier |
|---|---|---|---|---|---|---|
| win | 414 | 0.4682 | 0.3164 | +0.1517 | 🟡+32% | 0.2355 |

### 戦略別: 校正精度 + Brier Skill Score
| sid | bt | n | pred | actual | Brier | BSS | ROI |
|---|---|---|---|---|---|---|---|
| S00 | win | 179 | 0.4286 | 0.2737 | 0.2267 | 🔴-0.14 | 0.723 |
| S01_NAKAANA1 | win | 163 | 0.4786 | 0.2945 | 0.2374 | 🔴-0.14 | 0.813 |
| S02_TETSUBAN | win | 72 | 0.5428 | 0.4722 | 0.2531 | 🔴-0.02 | 0.946 |

### 確率デシル別: 校正カーブ
| 確率帯 | n | 予測avg | 実的中率 | gap |
|---|---|---|---|---|
| 0.15-0.20 | 7 | 0.1798 | 0.4286 | 🔴-0.2488 |
| 0.20-0.30 | 15 | 0.2268 | 0.2667 | ✅-0.0399 |
| 0.30-0.50 | 163 | 0.4176 | 0.2699 | 🔴+0.1477 |
| 0.50+ | 222 | 0.5420 | 0.3559 | 🔴+0.1861 |

## Settlement Ratio データ品質

- 学習済み: 4バンド / fallback: 13バンド
| bt | odds帯 | source | n | ratio |
|---|---|---|---|---|
| win | <3.0 | ✅learned | 80 | 0.811 |
| win | <5.0 | ✅learned | 150 | 0.722 |
| win | <10.0 | ✅learned | 76 | 0.464 |
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
_auto-generated by claude_snapshot.py at 2026-07-23T11:00:01.945158+09:00_