# ClaudeDebug スナップショット

## 🔴 現状: RED

**生成**: 2026-08-19T15:40:01.347987+09:00

### 次に取るべきアクション
> RED最優先: CIRCUIT_BREAKER_TRIP×22 (24h) → ログ/DB確認

### 検出された問題
- 🟡 FINAL_MISSING×46 (24h)
- 🔴 CIRCUIT_BREAKER_TRIP×22 (24h)
- 🔴 STRATEGY_CI_FAIL×17 (24h)
- 🟡 LARGE_ODDS_DRIFT×1 (24h)
- 🔴 alert_manager dispatch 失敗確定 1件（手動確認必要）

---

## 🔧 AI デバッグキュー（このClaudeが対処）

### 🔴 CIRCUIT_BREAKER_TRIP  ×36  [2026-08-19T15:04:43]
- key: `CIRCUIT_BREAKER_TRIP|`
- **FIX**: 7日ROI<0.7→戦略を enabled:false にして原因調査。校正ドリフトか市場変化を確認

### 🔴 CIRCUIT_BREAKER_NO_ACTION  ×72  [2026-08-19T15:04:43]
- key: `CIRCUIT_BREAKER_NO_ACTION|`
- **FIX**: CIRCUIT_BREAKER_TRIP 発動済なのに strategies.json で enabled のまま。enabled:false に切替 or 復旧条件満たしたか確認

### 🔴 STRATEGY_CI_FAIL  ×36  [2026-08-19T15:04:43]
- key: `STRATEGY_CI_FAIL|`
- **FIX**: grid戦略のOOS CI下限<1.0→論文基準で赤字リスク。strategies.json確認

### 🟡 ANOMALY_BET_VOLUME_DROP  ×10  [2026-08-19T15:01:05]
- key: `ANOMALY_BET_VOLUME_DROP|`
- **FIX**: 本日のbet数が7日baselineから2σ低下。戦略filter/ scan fix/run_cycle停止を疑え

### 🔴 CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION  ×3  [2026-08-19T14:30:04]
- key: `CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION|戦略 S00 が TRIP してるが enabled のまま`
- **FIX**: CIRCUIT_BREAKER_TRIP 戦略が enabled のまま。enabled:false に

### 🔴 CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION  ×3  [2026-08-19T14:30:04]
- key: `CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION|戦略 S02_TETSUBAN が TRIP してるが enabled のまま`
- **FIX**: CIRCUIT_BREAKER_TRIP 戦略が enabled のまま。enabled:false に

### 🟡 ANOMALY_SCRAPER_FAILURE_BURST  ×23  [2026-08-19T13:21:00]
- key: `ANOMALY_SCRAPER_FAILURE_BURST|`
- **FIX**: 直近1h でscraper 3-retry 全敗多発。boatrace.jp 側timeout / IP ban / DDoS

### 🟡 ANOMALY_SCAN_FINAL_RATIO  ×10  [2026-08-19T10:24:45]
- key: `ANOMALY_SCAN_FINAL_RATIO|`
- **FIX**: scan→final成立率が7日baselineから2σ逸脱。scan/final window設定・odds取得タイミング

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-08-19T06:00:11]
- key: `INSUFFICIENT_SAMPLE|S00: n=164<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-08-19T06:00:11]
- key: `INSUFFICIENT_SAMPLE|S02_TETSUBAN: n=75<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### 🟡 ORPHAN_SCAN  ×1  [2026-08-19T06:00:11]
- key: `ORPHAN_SCAN|194 件の scan に final/retreat 追従無し`
- **FIX**: scan 後 final も retreat も無い→当該レースの final 窓が短すぎ/fetch 失敗

### ℹ️ CALIBRATION_LIVE  ×1  [2026-08-19T06:00:11]
- key: `CALIBRATION_LIVE|decile 0.10-0.15: n=9 pred=0.1189 actual=0.1111 gap=+0.0078`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-08-19T06:00:11]
- key: `INSUFFICIENT_SAMPLE|S01_NAKAANA1: n=172<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ DRIFT_BUCKET  ×1  [2026-08-19T06:00:11]
- key: `DRIFT_BUCKET|drift ≤-30%: n=36 hit%=22.2% ROI=0.65 (コスト 10,400/回収 6,770)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ CALIBRATION_LIVE  ×1  [2026-08-19T06:00:11]
- key: `CALIBRATION_LIVE|decile 0.20-0.30: n=8 pred=0.2246 actual=0.3750 gap=-0.1504`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-08-19T06:00:11]
- key: `ROI_STAT|S00: n=164 hit%=24.4% hit_CI[Bonf]=[16.1,35.2]% ROI=0.77 ROI_boot95=[0.51,1.07]`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-08-19T06:00:11]
- key: `ROI_STAT|S01_NAKAANA1: n=172 hit%=23.3% hit_CI[Bonf]=[15.3,33.7]% ROI=0.82 ROI_boot95=[0.`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-08-19T06:00:11]
- key: `ROI_STAT|S02_TETSUBAN: n=75 hit%=46.7% hit_CI[Bonf]=[31.2,62.8]% ROI=0.72 ROI_boot95=[0.5`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ DRIFT_BUCKET  ×1  [2026-08-19T06:00:11]
- key: `DRIFT_BUCKET|drift -30%〜-10%: n=31 hit%=35.5% ROI=1.17 (コスト 7,300/回収 8,510)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-08-19T06:00:11]
- key: `DRIFT_BUCKET|drift -10%〜+10%: n=87 hit%=27.6% ROI=0.89 (コスト 20,200/回収 17,890)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料


以下、詳細セクション（通常読み飛ばし可）

## 環境・コード状態
- git_sha: `<error: Command '['git', '-C', '/opt/boa` dirty=True
- config.json md5: `eb532e851a30cd2f7e69bdf0dfca3f2b`
- strategies.json md5: `06b22dd935785e7947bf9c0f170b69a3`
- numpy=2.4.4 lightgbm=4.6.0 scipy=1.17.1
- **calibration_applied**: True ← predictor.py が校正を呼んでるか
- DB: 10.92MB / last modified 2026-08-19T15:39:37.695439+09:00

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
38:25,755 [INFO] run_cycle: fetched 15/2 [scan]: 153 combos
2026-08-19 15:38:26,045 [INFO] run_cycle: run_cycle done: 0 notifications
2026-08-19 15:39:04,140 [INFO] run_cycle: === run_cycle 15:39:04 ===
2026-08-19 15:39:04,140 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-08-19 15:39:04,140 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-08-19 15:39:04,194 [INFO] predictor: Models loaded OK
2026-08-19 15:39:15,383 [WARNING] scraper: fetch error (1/3): https://www.boatrace.jp/owpc/pc/race/racelist?rno=11&jcd=09&hd=20260819: HTTPSConnectionPool(host='www.boatrace.jp', port=443): Read timed out. (read timeout=10), retry in 1s
2026-08-19 15:39:26,832 [INFO] scraper: odds3t: 120/120 parsed
2026-08-19 15:39:27,904 [INFO] scraper: odds3f: 20/20 parsed
2026-08-19 15:39:28,994 [INFO] scraper: odds2t: 30/30 parsed
2026-08-19 15:39:28,995 [INFO] scraper: odds2f: 15/15 parsed
2026-08-19 15:39:30,089 [INFO] scraper: odds_win: 5/6 parsed
2026-08-19 15:39:30,090 [INFO] scraper: fetch_race 09/11: boats=6 odds=190/191
2026-08-19 15:39:30,093 [INFO] predictor: CALIBRATION_MODE=on
2026-08-19 15:39:30,093 [INFO] predictor: combos: {'win': 5, '2t': 30, '3t': 120}
2026-08-19 15:39:30,097 [INFO] run_cycle: fetched 09/11 [final]: 155 combos
2026-08-19 15:39:33,754 [INFO] scraper: odds3t: 120/120 parsed
2026-08-19 15:39:34,877 [INFO] scraper: odds3f: 20/20 parsed
2026-08-19 15:39:35,965 [INFO] scraper: odds2t: 30/30 parsed
2026-08-19 15:39:35,967 [INFO] scraper: odds2f: 14/15 parsed
2026-08-19 15:39:37,044 [INFO] scraper: odds_win: 3/6 parsed
2026-08-19 15:39:37,044 [INFO] scraper: fetch_race 11/11: boats=6 odds=187/191
2026-08-19 15:39:37,047 [INFO] predictor: CALIBRATION_MODE=on
2026-08-19 15:39:37,047 [INFO] predictor: combos: {'win': 3, '2t': 30, '3t': 120}
2026-08-19 15:39:37,050 [INFO] run_cycle: fetched 11/11 [scan]: 153 combos
2026-08-19 15:39:37,159 [INFO] run_cycle: run_cycle done: 0 notifications

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
    "c": 64
  },
  {
    "target": "primary",
    "ok": 1,
    "c": 64
  }
]
```

## Phase別通知記録 (24h)
{'final': 27, 'result': 12, 'scan': 25}

## アラート件数 (24h・種類別)
```
  ANOMALY_SCRAPER_FAILURE_BURST: 111
  FINAL_MISSING: 46
  CIRCUIT_BREAKER_NO_ACTION: 42
  CIRCUIT_BREAKER_TRIP: 22
  STRATEGY_CI_FAIL: 17
  ANOMALY_SCAN_FINAL_RATIO: 3
  ANOMALY_BET_VOLUME_DROP: 1
  LARGE_ODDS_DRIFT: 1
```

## 戦略別 ROI (7日)
| sid | n | hits | cost | payout | PL | ROI |
|---|---|---|---|---|---|---|
| S00 | 46 | 14 | 13,800 | 14,520 | +720 | 1.052 |
| S01_NAKAANA1 | 47 | 13 | 9,400 | 11,280 | +1,880 | 1.2 |
| S02_TETSUBAN | 20 | 4 | 4,000 | 1,060 | -2,940 | 0.265 |

## 直近アラート (24h・新しい順)
```
[15:36:20] CIRCUIT_BREAKER_TRIP: {"cost": 4000, "kind": "CIRCUIT_BREAKER_TRIP", "n": 20, "payout": 1060, "roi_7d": 0.265, "sid": "S02_TETSUBAN"}
[15:34:27] FINAL_MISSING: {"deadline": "2026-08-19T14:04:00+09:00", "kind": "FINAL_MISSING", "nid": "2026081905061404", "sid": "S00"}
[15:11:28] CIRCUIT_BREAKER_TRIP: {"cost": 4200, "kind": "CIRCUIT_BREAKER_TRIP", "n": 21, "payout": 1340, "roi_7d": 0.319, "sid": "S02_TETSUBAN"}
[15:11:28] LARGE_ODDS_DRIFT: {"combo": "1", "drift_pct": 23.8, "final": 2.6, "kind": "LARGE_ODDS_DRIFT", "race": "1110R", "scan": 2.1, "sid": "S02_TETSUBAN"}
[15:04:42] STRATEGY_CI_FAIL: {"ci_lo": null, "kind": "STRATEGY_CI_FAIL", "sid": "S02_TETSUBAN"}
[15:04:42] CIRCUIT_BREAKER_NO_ACTION: {"kind": "CIRCUIT_BREAKER_NO_ACTION", "sid": "S02_TETSUBAN"}
[15:04:42] CIRCUIT_BREAKER_NO_ACTION: {"kind": "CIRCUIT_BREAKER_NO_ACTION", "sid": "S00"}
[15:01:02] FINAL_MISSING: {"deadline": "2026-08-19T11:27:00+09:00", "kind": "FINAL_MISSING", "nid": "2026081914071127", "sid": "S00"}
[15:01:02] ANOMALY_BET_VOLUME_DROP: {"baseline_mean": 12.7, "baseline_n_days": 7, "baseline_stdev": 2.3, "hour": 15, "kind": "ANOMALY_BET_VOLUME_DROP", "today_so_far": 8, "z_score": -2.06}
[14:34:21] FINAL_MISSING: {"deadline": "2026-08-19T14:04:00+09:00", "kind": "FINAL_MISSING", "nid": "2026081905061404", "sid": "S00"}
```

## 本日残レース: 45件

## 本日nidレジャー（ID単位完遂突合せ）
- race_schedule: 144件 登録 / 99件 締切済
- 通知発射: scan=18 nid / final=17 nid / result=7 nid
- predictions: 9 / うち結果DB記録済: 8
- ✅ 結果DBあるが通知未発射: 0件 `tools/backfill_result_notifications.py` で救済可
- 🔴 scan後final無しのまま締切: 3件（FINAL_MISSING の温床）

## 直近送信失敗 (24h)
```
```

## 最新 predictions サンプル (計算spot-check用)
| sid | race | bt | combo | p | odds | ev | bet | at |
|---|---|---|---|---|---|---|---|---|
| S02_TETSUBAN | 1110R | win | 1 | 0.5123 | 2.6 | 1.33 | 200 | scan=2.1 drift=+23.8% | 15:11:20 |
| S01_NAKAANA1 | 056R | win | 1 | 0.5735 | 4.2 | 2.41 | 200 | scan=- drift=- | 14:02:19 |
| S01_NAKAANA1 | 137R | win | 1 | 0.5331 | 3.8 | 2.03 | 200 | scan=3.0 drift=+26.7% | 13:25:21 |
| S00 | 116R | win | 1 | 0.5476 | 7.5 | 4.11 | 300 | scan=5.2 drift=+44.2% | 13:05:19 |
| S01_NAKAANA1 | 135R | win | 1 | 0.2290 | 3.0 | 0.69 | 200 | scan=- drift=- | 12:21:31 |
| S00 | 135R | win | 1 | 0.2290 | 8.3 | 1.90 | 300 | scan=14.5 drift=-42.8% | 12:20:23 |
| S01_NAKAANA1 | 162R | win | 1 | 0.5334 | 3.5 | 1.87 | 200 | scan=- drift=- | 11:07:18 |
| S00 | 092R | win | 1 | 0.4111 | 12.0 | 4.93 | 300 | scan=12.0 drift=+0.0% | 10:57:31 |
| S00 | 131R | win | 1 | 0.5123 | 4.7 | 2.41 | 300 | scan=5.3 drift=-11.3% | 10:34:19 |
| S00 | 206R | win | 1 | 0.5334 | 4.2 | 2.24 | 300 | scan=- drift=- | 17:43:18 |

## オッズドリフト統計 (7日)

| bt | n | avg | min | max | down10 | collapse(≤-30%) | any_large(≥10%) |
|---|---|---|---|---|---|---|---|
| win | 69 | +5.9% | -62.9% | +207.5% | 14 | 7 | 32 |

## 校正テーブル合格状況

- total: 27 グループ
- passed: 19
- failed: 8 — `2f|4, 2f|5, 3f|2, 3f|3, 3f|4, 3t|1, 3t|4, 3t|5`
- 主力グループ状態: ✅ (全12グループ合格)

## SRE Golden Signals (24h)

| Signal | Value |
|---|---|
| **Latency** (scan→final avg) | 451.0s |
| **Latency** (scan→final max) | 616.0s |
| **Traffic** (notifications 24h) | 64 |
| **Errors** (send fail rate) | ✅ 0.0% |
| **Saturation** (S00) | 1,200円 used |
| **Saturation** (S01_NAKAANA1) | 800円 used |
| **Saturation** (S02_TETSUBAN) | 200円 used |

## 信ぴょう性メトリクス（予測精度の証拠）

### bt別: 予測確率 vs 実的中率
| bt | n | 予測avg | 実的中率 | 校正誤差 | 過信度 | Brier |
|---|---|---|---|---|---|---|
| win | 412 | 0.4661 | 0.2840 | +0.1821 | 🟡+39% | 0.2371 |

### 戦略別: 校正精度 + Brier Skill Score
| sid | bt | n | pred | actual | Brier | BSS | ROI |
|---|---|---|---|---|---|---|---|
| S00 | win | 164 | 0.4143 | 0.2500 | 0.2172 | 🔴-0.16 | 0.737 |
| S01_NAKAANA1 | win | 173 | 0.4869 | 0.2370 | 0.2519 | 🔴-0.39 | 0.829 |
| S02_TETSUBAN | win | 75 | 0.5313 | 0.4667 | 0.2465 | ✅+0.01 | 0.721 |

### 確率デシル別: 校正カーブ
| 確率帯 | n | 予測avg | 実的中率 | gap |
|---|---|---|---|---|
| 0.10-0.15 | 9 | 0.1189 | 0.1111 | ✅+0.0078 |
| 0.15-0.20 | 10 | 0.1830 | 0.0000 | 🔴+0.1830 |
| 0.20-0.30 | 10 | 0.2255 | 0.3000 | 🔴-0.0745 |
| 0.30-0.50 | 156 | 0.4138 | 0.2500 | 🔴+0.1638 |
| 0.50+ | 225 | 0.5429 | 0.3289 | 🔴+0.2140 |

## Settlement Ratio データ品質

- 学習済み: 4バンド / fallback: 13バンド
| bt | odds帯 | source | n | ratio |
|---|---|---|---|---|
| win | <3.0 | ✅learned | 112 | 0.765 |
| win | <5.0 | ✅learned | 200 | 0.757 |
| win | <10.0 | ✅learned | 99 | 0.446 |
| win | <20.0 | ✅learned | 30 | 0.227 |
| win | <50.0 | ⚠️fallback | 7 | 0.1 |
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
_auto-generated by claude_snapshot.py at 2026-08-19T15:40:01.347987+09:00_