# ClaudeDebug スナップショット

## 🔴 現状: RED

**生成**: 2026-09-19T14:30:02.300189+09:00

### 次に取るべきアクション
> RED最優先: PSI_DRIFT_DETECTED×44 (24h) → ログ/DB確認

### 検出された問題
- 🟡 FINAL_MISSING×88 (24h)
- 🔴 PSI_DRIFT_DETECTED×44 (24h)
- 🔴 CIRCUIT_BREAKER_TRIP×22 (24h)
- 🔴 STRATEGY_CI_FAIL×17 (24h)
- 🟡 LARGE_ODDS_DRIFT×2 (24h)
- 🔴 alert_manager dispatch 失敗確定 1件（手動確認必要）

---

## 🔧 AI デバッグキュー（このClaudeが対処）

### 🔴 CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION  ×1  [2026-09-19T14:30:03]
- key: `CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION|戦略 S00 が TRIP してるが enabled のまま`
- **FIX**: CIRCUIT_BREAKER_TRIP 戦略が enabled のまま。enabled:false に

### 🔴 CIRCUIT_BREAKER_TRIP  ×27  [2026-09-19T14:03:22]
- key: `CIRCUIT_BREAKER_TRIP|`
- **FIX**: 7日ROI<0.7→戦略を enabled:false にして原因調査。校正ドリフトか市場変化を確認

### 🔴 CIRCUIT_BREAKER_NO_ACTION  ×27  [2026-09-19T14:03:22]
- key: `CIRCUIT_BREAKER_NO_ACTION|`
- **FIX**: CIRCUIT_BREAKER_TRIP 発動済なのに strategies.json で enabled のまま。enabled:false に切替 or 復旧条件満たしたか確認

### 🔴 PSI_DRIFT_DETECTED  ×27  [2026-09-19T14:03:22]
- key: `PSI_DRIFT_DETECTED|`
- **FIX**: ml_prob 分布の PSI>0.25→モデル入力の分布シフト。校正テーブル再生成 or モデル再学習を検討

### 🔴 STRATEGY_CI_FAIL  ×27  [2026-09-19T14:03:22]
- key: `STRATEGY_CI_FAIL|`
- **FIX**: grid戦略のOOS CI下限<1.0→論文基準で赤字リスク。strategies.json確認

### 🟡 ANOMALY_SCAN_FINAL_RATIO  ×12  [2026-09-19T12:51:32]
- key: `ANOMALY_SCAN_FINAL_RATIO|`
- **FIX**: scan→final成立率が7日baselineから2σ逸脱。scan/final window設定・odds取得タイミング

### 🟡 ANOMALY_SCRAPER_FAILURE_BURST  ×10  [2026-09-19T12:06:19]
- key: `ANOMALY_SCRAPER_FAILURE_BURST|`
- **FIX**: 直近1h でscraper 3-retry 全敗多発。boatrace.jp 側timeout / IP ban / DDoS

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-09-19T06:00:19]
- key: `INSUFFICIENT_SAMPLE|S02_TETSUBAN: n=76<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-09-19T06:00:19]
- key: `INSUFFICIENT_SAMPLE|S00: n=175<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-09-19T06:00:19]
- key: `INSUFFICIENT_SAMPLE|S01_NAKAANA1: n=169<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ CALIBRATION_LIVE  ×1  [2026-09-19T06:00:19]
- key: `CALIBRATION_LIVE|decile 0.10-0.15: n=6 pred=0.1314 actual=0.0000 gap=+0.1314`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-09-19T06:00:19]
- key: `ROI_STAT|S00: n=175 hit%=24.6% hit_CI[Bonf]=[16.5,35.0]% ROI=0.76 ROI_boot95=[0.54,1.02]`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-09-19T06:00:19]
- key: `ROI_STAT|S01_NAKAANA1: n=169 hit%=24.3% hit_CI[Bonf]=[16.1,34.8]% ROI=0.70 ROI_boot95=[0.`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-09-19T06:00:19]
- key: `ROI_STAT|S02_TETSUBAN: n=76 hit%=40.8% hit_CI[Bonf]=[26.2,57.2]% ROI=0.76 ROI_boot95=[0.5`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### 🟡 ORPHAN_SCAN  ×1  [2026-09-19T06:00:19]
- key: `ORPHAN_SCAN|177 件の scan に final/retreat 追従無し`
- **FIX**: scan 後 final も retreat も無い→当該レースの final 窓が短すぎ/fetch 失敗

### ℹ️ DRIFT_BUCKET  ×1  [2026-09-19T06:00:19]
- key: `DRIFT_BUCKET|drift ≤-30%: n=33 hit%=30.3% ROI=0.88 (コスト 9,500/回収 8,390)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-09-19T06:00:19]
- key: `DRIFT_BUCKET|drift -30%〜-10%: n=44 hit%=20.5% ROI=0.55 (コスト 10,200/回収 5,560)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-09-19T06:00:19]
- key: `DRIFT_BUCKET|drift -10%〜+10%: n=81 hit%=22.2% ROI=0.68 (コスト 18,800/回収 12,810)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-09-19T06:00:19]
- key: `DRIFT_BUCKET|drift +10%〜+30%: n=45 hit%=24.4% ROI=0.51 (コスト 9,800/回収 5,040)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-09-19T06:00:19]
- key: `DRIFT_BUCKET|drift ≥+30%: n=42 hit%=11.9% ROI=0.43 (コスト 11,500/回収 4,990)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料


以下、詳細セクション（通常読み飛ばし可）

## 環境・コード状態
- git_sha: `<error: Command '['git', '-C', '/opt/boa` dirty=True
- config.json md5: `eb532e851a30cd2f7e69bdf0dfca3f2b`
- strategies.json md5: `06b22dd935785e7947bf9c0f170b69a3`
- numpy=2.4.4 lightgbm=4.6.0 scipy=1.17.1
- **calibration_applied**: True ← predictor.py が校正を呼んでるか
- DB: 13.63MB / last modified 2026-09-19T14:30:05.709918+09:00

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
2026-09-19 14:28:45,149 [INFO] scraper: odds2f: 15/15 parsed
2026-09-19 14:28:46,274 [INFO] scraper: odds_win: 6/6 parsed
2026-09-19 14:28:46,274 [INFO] scraper: fetch_race 05/9: boats=6 odds=191/191
2026-09-19 14:28:46,277 [INFO] predictor: CALIBRATION_MODE=on
2026-09-19 14:28:46,277 [INFO] predictor: combos: {'win': 6, '2t': 30, '3t': 120}
2026-09-19 14:28:46,280 [INFO] run_cycle: fetched 05/9 [scan]: 156 combos
2026-09-19 14:28:46,401 [INFO] run_cycle: run_cycle done: 0 notifications
2026-09-19 14:29:04,395 [INFO] run_cycle: === run_cycle 14:29:04 ===
2026-09-19 14:29:04,395 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-09-19 14:29:04,395 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-09-19 14:29:04,448 [INFO] predictor: Models loaded OK
2026-09-19 14:29:15,517 [WARNING] scraper: fetch error (1/3): https://www.boatrace.jp/owpc/pc/race/racelist?rno=7&jcd=06&hd=20260919: HTTPSConnectionPool(host='www.boatrace.jp', port=443): Read timed out. (read timeout=10), retry in 1s
2026-09-19 14:29:26,580 [WARNING] scraper: fetch error (2/3): https://www.boatrace.jp/owpc/pc/race/racelist?rno=7&jcd=06&hd=20260919: HTTPSConnectionPool(host='www.boatrace.jp', port=443): Read timed out. (read timeout=10), retry in 3s
2026-09-19 14:29:41,063 [INFO] scraper: odds3t: 120/120 parsed
2026-09-19 14:29:42,165 [INFO] scraper: odds3f: 20/20 parsed
2026-09-19 14:29:43,238 [INFO] scraper: odds2t: 30/30 parsed
2026-09-19 14:29:43,240 [INFO] scraper: odds2f: 15/15 parsed
2026-09-19 14:29:44,311 [INFO] scraper: odds_win: 5/6 parsed
2026-09-19 14:29:44,311 [INFO] scraper: fetch_race 06/7: boats=6 odds=190/191
2026-09-19 14:29:44,314 [INFO] predictor: CALIBRATION_MODE=on
2026-09-19 14:29:44,315 [INFO] predictor: combos: {'win': 5, '2t': 30, '3t': 120}
2026-09-19 14:29:44,318 [INFO] run_cycle: fetched 06/7 [final]: 155 combos
2026-09-19 14:29:44,675 [INFO] run_cycle: run_cycle done: 0 notifications

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
    "c": 65
  },
  {
    "target": "primary",
    "ok": 1,
    "c": 65
  }
]
```

## Phase別通知記録 (24h)
{'final': 25, 'result': 14, 'scan': 26}

## アラート件数 (24h・種類別)
```
  ANOMALY_SCRAPER_FAILURE_BURST: 223
  FINAL_MISSING: 88
  PSI_DRIFT_DETECTED: 44
  CIRCUIT_BREAKER_TRIP: 22
  CIRCUIT_BREAKER_NO_ACTION: 17
  STRATEGY_CI_FAIL: 17
  ANOMALY_SCAN_FINAL_RATIO: 10
  LARGE_ODDS_DRIFT: 2
```

## 戦略別 ROI (7日)
| sid | n | hits | cost | payout | PL | ROI |
|---|---|---|---|---|---|---|
| S00 | 43 | 10 | 12,900 | 8,430 | -4,470 | 0.653 |
| S01_NAKAANA1 | 34 | 11 | 6,800 | 7,700 | +900 | 1.132 |
| S02_TETSUBAN | 17 | 9 | 3,400 | 3,680 | +280 | 1.082 |

## 直近アラート (24h・新しい順)
```
[14:29:44] PSI_DRIFT_DETECTED: {"bt": "win", "kind": "PSI_DRIFT_DETECTED", "n_baseline": 325, "n_recent": 94, "psi": 0.422}
[14:28:46] FINAL_MISSING: {"deadline": "2026-09-19T11:57:00+09:00", "kind": "FINAL_MISSING", "nid": "2026091905041157", "sid": "S00"}
[14:23:27] PSI_DRIFT_DETECTED: {"bt": "win", "kind": "PSI_DRIFT_DETECTED", "n_baseline": 324, "n_recent": 95, "psi": 0.424}
[14:22:34] FINAL_MISSING: {"deadline": "2026-09-19T13:52:00+09:00", "kind": "FINAL_MISSING", "nid": "2026091916071352", "sid": "S00"}
[14:13:30] PSI_DRIFT_DETECTED: {"bt": "win", "kind": "PSI_DRIFT_DETECTED", "n_baseline": 325, "n_recent": 95, "psi": 0.427}
[14:13:30] LARGE_ODDS_DRIFT: {"combo": "1", "drift_pct": 18.7, "final": 3.8, "kind": "LARGE_ODDS_DRIFT", "race": "028R", "scan": 3.2, "sid": "S01_NAKAANA1"}
[14:03:22] STRATEGY_CI_FAIL: {"ci_lo": null, "kind": "STRATEGY_CI_FAIL", "sid": "S02_TETSUBAN"}
[14:03:22] CIRCUIT_BREAKER_NO_ACTION: {"kind": "CIRCUIT_BREAKER_NO_ACTION", "sid": "S00"}
[13:57:26] CIRCUIT_BREAKER_TRIP: {"cost": 12900, "kind": "CIRCUIT_BREAKER_TRIP", "n": 43, "payout": 8430, "roi_7d": 0.653, "sid": "S00"}
[13:57:26] FINAL_MISSING: {"deadline": "2026-09-19T13:27:00+09:00", "kind": "FINAL_MISSING", "nid": "2026091913071327", "sid": "S02_TETSUBAN"}
```

## 本日残レース: 70件

## 本日nidレジャー（ID単位完遂突合せ）
- race_schedule: 156件 登録 / 86件 締切済
- 通知発射: scan=18 nid / final=16 nid / result=10 nid
- predictions: 11 / うち結果DB記録済: 10
- ✅ 結果DBあるが通知未発射: 0件 `tools/backfill_result_notifications.py` で救済可
- 🔴 scan後final無しのまま締切: 6件（FINAL_MISSING の温床）

## 直近送信失敗 (24h)
```
```

## 最新 predictions サンプル (計算spot-check用)
| sid | race | bt | combo | p | odds | ev | bet | at |
|---|---|---|---|---|---|---|---|---|
| S01_NAKAANA1 | 028R | win | 1 | 0.3177 | 3.8 | 1.21 | 200 | scan=3.2 drift=+18.7% | 14:13:18 |
| S02_TETSUBAN | 037R | win | 1 | 0.5735 | 2.0 | 1.15 | 200 | scan=2.1 drift=-4.8% | 13:53:19 |
| S00 | 036R | win | 1 | 0.5322 | 5.2 | 2.77 | 300 | scan=- drift=- | 13:26:18 |
| S00 | 046R | win | 1 | 0.5476 | 7.2 | 3.94 | 300 | scan=5.8 drift=+24.1% | 13:19:31 |
| S01_NAKAANA1 | 044R | win | 1 | 0.4111 | 4.9 | 2.01 | 200 | scan=- drift=- | 12:19:18 |
| S02_TETSUBAN | 054R | win | 1 | 0.5123 | 2.1 | 1.08 | 200 | scan=- drift=- | 11:54:44 |
| S00 | 032R | win | 1 | 0.5334 | 5.6 | 2.99 | 300 | scan=4.8 drift=+16.7% | 11:38:31 |
| S00 | 173R | win | 1 | 0.4111 | 6.6 | 2.71 | 300 | scan=36.1 drift=-81.7% | 11:34:20 |
| S02_TETSUBAN | 053R | win | 1 | 0.5083 | 2.5 | 1.27 | 200 | scan=2.1 drift=+19.0% | 11:24:30 |
| S01_NAKAANA1 | 145R | win | 1 | 0.5735 | 3.8 | 2.18 | 200 | scan=- drift=- | 10:13:18 |

## オッズドリフト統計 (7日)

| bt | n | avg | min | max | down10 | collapse(≤-30%) | any_large(≥10%) |
|---|---|---|---|---|---|---|---|
| win | 57 | +3.0% | -81.7% | +119.5% | 14 | 5 | 34 |

## 校正テーブル合格状況

- total: 27 グループ
- passed: 19
- failed: 8 — `2f|4, 2f|5, 3f|2, 3f|3, 3f|4, 3t|1, 3t|4, 3t|5`
- 主力グループ状態: ✅ (全12グループ合格)

## SRE Golden Signals (24h)

| Signal | Value |
|---|---|
| **Latency** (scan→final avg) | 440.2s |
| **Latency** (scan→final max) | 606.7s |
| **Traffic** (notifications 24h) | 65 |
| **Errors** (send fail rate) | ✅ 0.0% |
| **Saturation** (S00) | 1,200円 used |
| **Saturation** (S01_NAKAANA1) | 800円 used |
| **Saturation** (S02_TETSUBAN) | 600円 used |

## 信ぴょう性メトリクス（予測精度の証拠）

### bt別: 予測確率 vs 実的中率
| bt | n | 予測avg | 実的中率 | 校正誤差 | 過信度 | Brier |
|---|---|---|---|---|---|---|
| win | 418 | 0.4788 | 0.2656 | +0.2133 | 🟡+44% | 0.2410 |

### 戦略別: 校正精度 + Brier Skill Score
| sid | bt | n | pred | actual | Brier | BSS | ROI |
|---|---|---|---|---|---|---|---|
| S00 | win | 172 | 0.4421 | 0.2384 | 0.2267 | 🔴-0.25 | 0.741 |
| S01_NAKAANA1 | win | 170 | 0.4880 | 0.2294 | 0.2455 | 🔴-0.39 | 0.66 |
| S02_TETSUBAN | win | 76 | 0.5414 | 0.4079 | 0.2634 | 🔴-0.09 | 0.75 |

### 確率デシル別: 校正カーブ
| 確率帯 | n | 予測avg | 実的中率 | gap |
|---|---|---|---|---|
| 0.10-0.15 | 6 | 0.1314 | 0.0000 | 🔴+0.1314 |
| 0.30-0.50 | 149 | 0.4098 | 0.2215 | 🔴+0.1884 |
| 0.50+ | 250 | 0.5452 | 0.3040 | 🔴+0.2412 |

## Settlement Ratio データ品質

- 学習済み: 4バンド / fallback: 13バンド
| bt | odds帯 | source | n | ratio |
|---|---|---|---|---|
| win | <3.0 | ✅learned | 145 | 0.775 |
| win | <5.0 | ✅learned | 256 | 0.761 |
| win | <10.0 | ✅learned | 125 | 0.46 |
| win | <20.0 | ✅learned | 33 | 0.234 |
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
_auto-generated by claude_snapshot.py at 2026-09-19T14:30:02.300189+09:00_