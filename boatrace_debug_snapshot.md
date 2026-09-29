# ClaudeDebug スナップショット

## 🔴 現状: RED

**生成**: 2026-09-29T16:30:01.870866+09:00

### 次に取るべきアクション
> RED最優先: CIRCUIT_BREAKER_TRIP×45 (24h) → ログ/DB確認

### 検出された問題
- 🟡 FINAL_MISSING×90 (24h)
- 🔴 CIRCUIT_BREAKER_TRIP×45 (24h)
- 🔴 STRATEGY_CI_FAIL×17 (24h)
- 🔴 PSI_DRIFT_DETECTED×9 (24h)
- 🟡 LARGE_ODDS_DRIFT×2 (24h)
- 🔴 alert_manager dispatch 失敗確定 1件（手動確認必要）

---

## 🔧 AI デバッグキュー（このClaudeが対処）

### 🔴 PSI_DRIFT_DETECTED  ×7  [2026-09-29T16:23:35]
- key: `PSI_DRIFT_DETECTED|`
- **FIX**: ml_prob 分布の PSI>0.25→モデル入力の分布シフト。校正テーブル再生成 or モデル再学習を検討

### 🔴 CIRCUIT_BREAKER_TRIP  ×24  [2026-09-29T16:06:22]
- key: `CIRCUIT_BREAKER_TRIP|`
- **FIX**: 7日ROI<0.7→戦略を enabled:false にして原因調査。校正ドリフトか市場変化を確認

### 🔴 CIRCUIT_BREAKER_NO_ACTION  ×48  [2026-09-29T16:06:22]
- key: `CIRCUIT_BREAKER_NO_ACTION|`
- **FIX**: CIRCUIT_BREAKER_TRIP 発動済なのに strategies.json で enabled のまま。enabled:false に切替 or 復旧条件満たしたか確認

### 🔴 STRATEGY_CI_FAIL  ×24  [2026-09-29T16:06:22]
- key: `STRATEGY_CI_FAIL|`
- **FIX**: grid戦略のOOS CI下限<1.0→論文基準で赤字リスク。strategies.json確認

### 🟡 CODE_AUDIT_SCRAPER_FAILURE_RATE_HIGH  ×1  [2026-09-29T16:00:03]
- key: `CODE_AUDIT_SCRAPER_FAILURE_RATE_HIGH|直近 500 log行 で 3-retry 全敗 4 件 (閾値 3)`
- **FIX**: scraper 3-retry 全敗多発。boatrace.jp timeout or IP ban 疑い

### 🟡 ANOMALY_SCRAPER_FAILURE_BURST  ×49  [2026-09-29T15:41:11]
- key: `ANOMALY_SCRAPER_FAILURE_BURST|`
- **FIX**: 直近1h でscraper 3-retry 全敗多発。boatrace.jp 側timeout / IP ban / DDoS

### 🔴 CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION  ×3  [2026-09-29T15:00:05]
- key: `CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION|戦略 S00 が TRIP してるが enabled のまま`
- **FIX**: CIRCUIT_BREAKER_TRIP 戦略が enabled のまま。enabled:false に

### 🔴 CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION  ×3  [2026-09-29T15:00:05]
- key: `CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION|戦略 S01_NAKAANA1 が TRIP してるが enabled のまま`
- **FIX**: CIRCUIT_BREAKER_TRIP 戦略が enabled のまま。enabled:false に

### 🟡 ANOMALY_BET_VOLUME_SPIKE  ×7  [2026-09-29T13:53:20]
- key: `ANOMALY_BET_VOLUME_SPIKE|`
- **FIX**: 本日のbet数が2σ急増。filter logic緩み・戦略追加・race_schedule異常

### 🟡 ANOMALY_SCAN_FINAL_RATIO  ×11  [2026-09-29T11:48:38]
- key: `ANOMALY_SCAN_FINAL_RATIO|`
- **FIX**: scan→final成立率が7日baselineから2σ逸脱。scan/final window設定・odds取得タイミング

### 🟡 ANOMALY_BET_VOLUME_DROP  ×22  [2026-09-29T11:01:28]
- key: `ANOMALY_BET_VOLUME_DROP|`
- **FIX**: 本日のbet数が7日baselineから2σ低下。戦略filter/ scan fix/run_cycle停止を疑え

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-09-29T06:00:18]
- key: `INSUFFICIENT_SAMPLE|S02_TETSUBAN: n=77<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-09-29T06:00:18]
- key: `INSUFFICIENT_SAMPLE|S00: n=163<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### 🟡 ORPHAN_SCAN  ×1  [2026-09-29T06:00:18]
- key: `ORPHAN_SCAN|170 件の scan に final/retreat 追従無し`
- **FIX**: scan 後 final も retreat も無い→当該レースの final 窓が短すぎ/fetch 失敗

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-09-29T06:00:18]
- key: `INSUFFICIENT_SAMPLE|S01_NAKAANA1: n=155<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ DRIFT_BUCKET  ×1  [2026-09-29T06:00:18]
- key: `DRIFT_BUCKET|drift ≤-30%: n=28 hit%=32.1% ROI=0.94 (コスト 7,900/回収 7,430)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ ROI_STAT  ×1  [2026-09-29T06:00:18]
- key: `ROI_STAT|S00: n=163 hit%=21.5% hit_CI[Bonf]=[13.7,32.0]% ROI=0.64 ROI_boot95=[0.41,0.92]`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-09-29T06:00:18]
- key: `ROI_STAT|S01_NAKAANA1: n=155 hit%=21.9% hit_CI[Bonf]=[13.9,32.8]% ROI=0.66 ROI_boot95=[0.`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-09-29T06:00:18]
- key: `ROI_STAT|S02_TETSUBAN: n=77 hit%=49.4% hit_CI[Bonf]=[33.8,65.0]% ROI=0.87 ROI_boot95=[0.6`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ DRIFT_BUCKET  ×1  [2026-09-29T06:00:18]
- key: `DRIFT_BUCKET|drift -30%〜-10%: n=40 hit%=25.0% ROI=0.69 (コスト 9,100/回収 6,270)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料


以下、詳細セクション（通常読み飛ばし可）

## 環境・コード状態
- git_sha: `<error: Command '['git', '-C', '/opt/boa` dirty=True
- config.json md5: `eb532e851a30cd2f7e69bdf0dfca3f2b`
- strategies.json md5: `06b22dd935785e7947bf9c0f170b69a3`
- numpy=2.4.4 lightgbm=4.6.0 scipy=1.17.1
- **calibration_applied**: True ← predictor.py が校正を呼んでるか
- DB: 14.48MB / last modified 2026-09-29T16:29:47.937203+09:00

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
30/30 parsed
2026-09-29 16:28:25,931 [INFO] scraper: odds2f: 15/15 parsed
2026-09-29 16:28:27,085 [INFO] scraper: odds_win: 6/6 parsed
2026-09-29 16:28:27,085 [INFO] scraper: fetch_race 04/12: boats=6 odds=191/191
2026-09-29 16:28:27,088 [INFO] predictor: CALIBRATION_MODE=on
2026-09-29 16:28:27,088 [INFO] predictor: combos: {'win': 6, '2t': 30, '3t': 120}
2026-09-29 16:28:27,093 [INFO] run_cycle: fetched 04/12 [scan]: 156 combos
2026-09-29 16:28:27,284 [INFO] run_cycle: run_cycle done: 0 notifications
2026-09-29 16:29:05,187 [INFO] run_cycle: === run_cycle 16:29:05 ===
2026-09-29 16:29:05,187 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-09-29 16:29:05,187 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-09-29 16:29:05,228 [INFO] predictor: Models loaded OK
2026-09-29 16:29:16,609 [WARNING] scraper: fetch error (1/3): https://www.boatrace.jp/owpc/pc/race/racelist?rno=4&jcd=07&hd=20260929: HTTPSConnectionPool(host='www.boatrace.jp', port=443): Read timed out. (read timeout=10), retry in 1s
2026-09-29 16:29:27,990 [WARNING] scraper: fetch error (2/3): https://www.boatrace.jp/owpc/pc/race/racelist?rno=4&jcd=07&hd=20260929: HTTPSConnectionPool(host='www.boatrace.jp', port=443): Read timed out. (read timeout=10), retry in 3s
2026-09-29 16:29:41,617 [INFO] scraper: odds3t: 120/120 parsed
2026-09-29 16:29:42,723 [INFO] scraper: odds3f: 20/20 parsed
2026-09-29 16:29:43,944 [INFO] scraper: odds2t: 28/30 parsed
2026-09-29 16:29:43,945 [INFO] scraper: odds2f: 15/15 parsed
2026-09-29 16:29:45,046 [INFO] scraper: odds_win: 6/6 parsed
2026-09-29 16:29:45,046 [INFO] scraper: fetch_race 07/4: boats=6 odds=189/191
2026-09-29 16:29:45,054 [INFO] predictor: CALIBRATION_MODE=on
2026-09-29 16:29:45,054 [INFO] predictor: combos: {'win': 6, '2t': 28, '3t': 120}
2026-09-29 16:29:45,060 [INFO] run_cycle: fetched 07/4 [scan]: 154 combos
2026-09-29 16:29:45,229 [INFO] run_cycle: run_cycle done: 0 notifications

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
    "c": 74
  },
  {
    "target": "primary",
    "ok": 1,
    "c": 74
  }
]
```

## Phase別通知記録 (24h)
{'final': 27, 'result': 18, 'scan': 29}

## アラート件数 (24h・種類別)
```
  ANOMALY_SCRAPER_FAILURE_BURST: 102
  FINAL_MISSING: 90
  CIRCUIT_BREAKER_TRIP: 45
  CIRCUIT_BREAKER_NO_ACTION: 34
  STRATEGY_CI_FAIL: 17
  ANOMALY_SCAN_FINAL_RATIO: 14
  PSI_DRIFT_DETECTED: 9
  ANOMALY_BET_VOLUME_SPIKE: 6
  ANOMALY_BET_VOLUME_DROP: 3
  LARGE_ODDS_DRIFT: 2
```

## 戦略別 ROI (7日)
| sid | n | hits | cost | payout | PL | ROI |
|---|---|---|---|---|---|---|
| S00 | 40 | 6 | 12,000 | 4,470 | -7,530 | 0.372 |
| S01_NAKAANA1 | 38 | 11 | 7,600 | 5,360 | -2,240 | 0.705 |
| S02_TETSUBAN | 24 | 15 | 4,800 | 5,160 | +360 | 1.075 |

## 直近アラート (24h・新しい順)
```
[16:29:45] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 6, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1080}
[16:28:27] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 6, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1096}
[16:27:27] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 6, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1089}
[16:26:05] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 6, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1088}
[16:25:20] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 6, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1098}
[16:23:35] CIRCUIT_BREAKER_TRIP: {"cost": 12000, "kind": "CIRCUIT_BREAKER_TRIP", "n": 40, "payout": 4470, "roi_7d": 0.372, "sid": "S00"}
[16:23:35] FINAL_MISSING: {"deadline": "2026-09-29T10:51:00+09:00", "kind": "FINAL_MISSING", "nid": "2026092914061051", "sid": "S00"}
[16:22:27] PSI_DRIFT_DETECTED: {"bt": "win", "kind": "PSI_DRIFT_DETECTED", "n_baseline": 304, "n_recent": 102, "psi": 0.389}
[16:22:27] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 7, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1080}
[16:21:45] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 7, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1061}
```

## 本日残レース: 42件

## 本日nidレジャー（ID単位完遂突合せ）
- race_schedule: 144件 登録 / 102件 締切済
- 通知発射: scan=24 nid / final=22 nid / result=15 nid
- predictions: 18 / うち結果DB記録済: 17
- ✅ 結果DBあるが通知未発射: 0件 `tools/backfill_result_notifications.py` で救済可
- 🔴 scan後final無しのまま締切: 7件（FINAL_MISSING の温床）

## 直近送信失敗 (24h)
```
```

## 最新 predictions サンプル (計算spot-check用)
| sid | race | bt | combo | p | odds | ev | bet | at |
|---|---|---|---|---|---|---|---|---|
| S01_NAKAANA1 | 153R | win | 1 | 0.3177 | 4.3 | 1.37 | 200 | scan=4.7 drift=-8.5% | 16:03:32 |
| S01_NAKAANA1 | 0211R | win | 1 | 0.4111 | 3.4 | 1.40 | 200 | scan=3.0 drift=+13.3% | 15:52:31 |
| S02_TETSUBAN | 168R | win | 1 | 0.4989 | 2.7 | 1.35 | 200 | scan=2.3 drift=+17.4% | 14:35:31 |
| S01_NAKAANA1 | 056R | win | 1 | 0.4111 | 3.3 | 1.36 | 200 | scan=3.9 drift=-15.4% | 13:30:23 |
| S01_NAKAANA1 | 026R | win | 1 | 0.5891 | 4.2 | 2.47 | 200 | scan=3.4 drift=+23.5% | 13:11:20 |
| S01_NAKAANA1 | 055R | win | 1 | 0.4111 | 4.5 | 1.85 | 200 | scan=- drift=- | 12:59:46 |
| S00 | 055R | win | 1 | 0.4111 | 4.5 | 1.85 | 300 | scan=- drift=- | 12:59:44 |
| S01_NAKAANA1 | 219R | win | 1 | 0.5334 | 3.1 | 1.65 | 200 | scan=4.9 drift=-36.7% | 12:38:21 |
| S01_NAKAANA1 | 044R | win | 1 | 0.5123 | 4.5 | 2.31 | 200 | scan=- drift=- | 12:21:19 |
| S01_NAKAANA1 | 024R | win | 1 | 0.5719 | 4.0 | 2.29 | 200 | scan=3.7 drift=+8.1% | 12:11:28 |

## オッズドリフト統計 (7日)

| bt | n | avg | min | max | down10 | collapse(≤-30%) | any_large(≥10%) |
|---|---|---|---|---|---|---|---|
| win | 65 | +7.6% | -72.2% | +357.1% | 21 | 7 | 41 |

## 校正テーブル合格状況

- total: 27 グループ
- passed: 19
- failed: 8 — `2f|4, 2f|5, 3f|2, 3f|3, 3f|4, 3t|1, 3t|4, 3t|5`
- 主力グループ状態: ✅ (全12グループ合格)

## SRE Golden Signals (24h)

| Signal | Value |
|---|---|
| **Latency** (scan→final avg) | 445.1s |
| **Latency** (scan→final max) | 617.8s |
| **Traffic** (notifications 24h) | 74 |
| **Errors** (send fail rate) | ✅ 0.0% |
| **Saturation** (S00) | 1,500円 used |
| **Saturation** (S01_NAKAANA1) | 2,400円 used |
| **Saturation** (S02_TETSUBAN) | 200円 used |

## 信ぴょう性メトリクス（予測精度の証拠）

### bt別: 予測確率 vs 実的中率
| bt | n | 予測avg | 実的中率 | 校正誤差 | 過信度 | Brier |
|---|---|---|---|---|---|---|
| win | 405 | 0.4804 | 0.2741 | +0.2063 | 🟡+43% | 0.2454 |

### 戦略別: 校正精度 + Brier Skill Score
| sid | bt | n | pred | actual | Brier | BSS | ROI |
|---|---|---|---|---|---|---|---|
| S00 | win | 164 | 0.4502 | 0.2134 | 0.2377 | 🔴-0.42 | 0.637 |
| S01_NAKAANA1 | win | 164 | 0.4901 | 0.2317 | 0.2491 | 🔴-0.40 | 0.68 |
| S02_TETSUBAN | win | 77 | 0.5242 | 0.4935 | 0.2538 | 🔴-0.02 | 0.843 |

### 確率デシル別: 校正カーブ
| 確率帯 | n | 予測avg | 実的中率 | gap |
|---|---|---|---|---|
| 0.30-0.50 | 151 | 0.4145 | 0.2318 | 🔴+0.1827 |
| 0.50+ | 239 | 0.5439 | 0.3054 | 🔴+0.2385 |

## Settlement Ratio データ品質

- 学習済み: 4バンド / fallback: 13バンド
| bt | odds帯 | source | n | ratio |
|---|---|---|---|---|
| win | <3.0 | ✅learned | 163 | 0.771 |
| win | <5.0 | ✅learned | 277 | 0.752 |
| win | <10.0 | ✅learned | 126 | 0.46 |
| win | <20.0 | ✅learned | 34 | 0.237 |
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
_auto-generated by claude_snapshot.py at 2026-09-29T16:30:01.870866+09:00_