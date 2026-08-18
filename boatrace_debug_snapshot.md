# ClaudeDebug スナップショット

## 🔴 現状: RED

**生成**: 2026-08-18T11:30:01.615195+09:00

### 次に取るべきアクション
> RED最優先: CIRCUIT_BREAKER_TRIP×55 (24h) → ログ/DB確認

### 検出された問題
- 🔴 CIRCUIT_BREAKER_TRIP×55 (24h)
- 🟡 FINAL_MISSING×25 (24h)
- 🔴 STRATEGY_CI_FAIL×17 (24h)
- 🟡 LARGE_ODDS_DRIFT×1 (24h)
- 🔴 alert_manager dispatch 失敗確定 1件（手動確認必要）

---

## 🔧 AI デバッグキュー（このClaudeが対処）

### 🔴 CIRCUIT_BREAKER_TRIP  ×52  [2026-08-18T11:02:30]
- key: `CIRCUIT_BREAKER_TRIP|`
- **FIX**: 7日ROI<0.7→戦略を enabled:false にして原因調査。校正ドリフトか市場変化を確認

### 🔴 CIRCUIT_BREAKER_NO_ACTION  ×78  [2026-08-18T11:02:30]
- key: `CIRCUIT_BREAKER_NO_ACTION|`
- **FIX**: CIRCUIT_BREAKER_TRIP 発動済なのに strategies.json で enabled のまま。enabled:false に切替 or 復旧条件満たしたか確認

### 🔴 STRATEGY_CI_FAIL  ×26  [2026-08-18T11:02:30]
- key: `STRATEGY_CI_FAIL|`
- **FIX**: grid戦略のOOS CI下限<1.0→論文基準で赤字リスク。strategies.json確認

### 🟡 ANOMALY_SCRAPER_FAILURE_BURST  ×28  [2026-08-18T10:50:15]
- key: `ANOMALY_SCRAPER_FAILURE_BURST|`
- **FIX**: 直近1h でscraper 3-retry 全敗多発。boatrace.jp 側timeout / IP ban / DDoS

### 🟡 ANOMALY_SCAN_FINAL_RATIO  ×26  [2026-08-18T10:47:27]
- key: `ANOMALY_SCAN_FINAL_RATIO|`
- **FIX**: scan→final成立率が7日baselineから2σ逸脱。scan/final window設定・odds取得タイミング

### 🔴 CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION  ×3  [2026-08-18T10:30:04]
- key: `CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION|戦略 S00 が TRIP してるが enabled のまま`
- **FIX**: CIRCUIT_BREAKER_TRIP 戦略が enabled のまま。enabled:false に

### 🔴 CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION  ×3  [2026-08-18T10:30:04]
- key: `CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION|戦略 S01_NAKAANA1 が TRIP してるが enabled のまま`
- **FIX**: CIRCUIT_BREAKER_TRIP 戦略が enabled のまま。enabled:false に

### 🔴 CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION  ×3  [2026-08-18T10:30:04]
- key: `CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION|戦略 S02_TETSUBAN が TRIP してるが enabled のまま`
- **FIX**: CIRCUIT_BREAKER_TRIP 戦略が enabled のまま。enabled:false に

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-08-18T06:00:19]
- key: `INSUFFICIENT_SAMPLE|S02_TETSUBAN: n=74<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### 🟡 ORPHAN_SCAN  ×1  [2026-08-18T06:00:19]
- key: `ORPHAN_SCAN|205 件の scan に final/retreat 追従無し`
- **FIX**: scan 後 final も retreat も無い→当該レースの final 窓が短すぎ/fetch 失敗

### ℹ️ CALIBRATION_LIVE  ×1  [2026-08-18T06:00:19]
- key: `CALIBRATION_LIVE|decile 0.10-0.15: n=9 pred=0.1189 actual=0.1111 gap=+0.0078`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-08-18T06:00:19]
- key: `CALIBRATION_LIVE|decile 0.15-0.20: n=12 pred=0.1827 actual=0.0833 gap=+0.0994`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-08-18T06:00:19]
- key: `ROI_STAT|S00: n=166 hit%=22.9% hit_CI[Bonf]=[14.9,33.5]% ROI=0.64 ROI_boot95=[0.43,0.86]`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-08-18T06:00:19]
- key: `INSUFFICIENT_SAMPLE|S00: n=166<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ ROI_STAT  ×1  [2026-08-18T06:00:19]
- key: `ROI_STAT|S01_NAKAANA1: n=172 hit%=22.7% hit_CI[Bonf]=[14.8,33.0]% ROI=0.74 ROI_boot95=[0.`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-08-18T06:00:19]
- key: `INSUFFICIENT_SAMPLE|S01_NAKAANA1: n=172<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ ROI_STAT  ×1  [2026-08-18T06:00:19]
- key: `ROI_STAT|S02_TETSUBAN: n=74 hit%=47.3% hit_CI[Bonf]=[31.7,63.5]% ROI=0.73 ROI_boot95=[0.5`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ DRIFT_BUCKET  ×1  [2026-08-18T06:00:19]
- key: `DRIFT_BUCKET|drift ≤-30%: n=36 hit%=22.2% ROI=0.65 (コスト 10,400/回収 6,770)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-08-18T06:00:19]
- key: `DRIFT_BUCKET|drift -30%〜-10%: n=34 hit%=35.3% ROI=1.08 (コスト 8,100/回収 8,770)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-08-18T06:00:19]
- key: `DRIFT_BUCKET|drift -10%〜+10%: n=82 hit%=26.8% ROI=0.64 (コスト 19,300/回収 12,390)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料


以下、詳細セクション（通常読み飛ばし可）

## 環境・コード状態
- git_sha: `<error: Command '['git', '-C', '/opt/boa` dirty=True
- config.json md5: `eb532e851a30cd2f7e69bdf0dfca3f2b`
- strategies.json md5: `06b22dd935785e7947bf9c0f170b69a3`
- numpy=2.4.4 lightgbm=4.6.0 scipy=1.17.1
- **calibration_applied**: True ← predictor.py が校正を呼んでるか
- DB: 10.79MB / last modified 2026-08-18T11:30:05.010636+09:00

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
 combos: {'win': 5, '2t': 29, '3t': 120}
2026-08-18 11:28:42,487 [INFO] run_cycle: fetched 11/3 [final]: 154 combos
2026-08-18 11:28:45,924 [INFO] scraper: odds3t: 120/120 parsed
2026-08-18 11:28:47,036 [INFO] scraper: odds3f: 20/20 parsed
2026-08-18 11:28:48,114 [INFO] scraper: odds2t: 30/30 parsed
2026-08-18 11:28:48,115 [INFO] scraper: odds2f: 15/15 parsed
2026-08-18 11:28:49,181 [INFO] scraper: odds_win: 5/6 parsed
2026-08-18 11:28:49,181 [INFO] scraper: fetch_race 13/3: boats=6 odds=190/191
2026-08-18 11:28:49,184 [INFO] predictor: CALIBRATION_MODE=on
2026-08-18 11:28:49,184 [INFO] predictor: combos: {'win': 5, '2t': 30, '3t': 120}
2026-08-18 11:28:49,188 [INFO] run_cycle: fetched 13/3 [final]: 155 combos
2026-08-18 11:28:52,638 [INFO] scraper: odds3t: 120/120 parsed
2026-08-18 11:28:53,719 [INFO] scraper: odds3f: 20/20 parsed
2026-08-18 11:28:54,817 [INFO] scraper: odds2t: 30/30 parsed
2026-08-18 11:28:54,818 [INFO] scraper: odds2f: 15/15 parsed
2026-08-18 11:28:55,884 [INFO] scraper: odds_win: 6/6 parsed
2026-08-18 11:28:55,884 [INFO] scraper: fetch_race 05/1: boats=6 odds=191/191
2026-08-18 11:28:55,887 [INFO] predictor: CALIBRATION_MODE=on
2026-08-18 11:28:55,887 [INFO] predictor: combos: {'win': 6, '2t': 30, '3t': 120}
2026-08-18 11:28:55,891 [INFO] run_cycle: fetched 05/1 [scan]: 156 combos
2026-08-18 11:28:59,296 [INFO] scraper: odds3t: 120/120 parsed
2026-08-18 11:29:00,377 [INFO] scraper: odds3f: 20/20 parsed
2026-08-18 11:29:01,494 [INFO] scraper: odds2t: 29/30 parsed
2026-08-18 11:29:01,495 [INFO] scraper: odds2f: 15/15 parsed
2026-08-18 11:29:02,572 [INFO] scraper: odds_win: 4/6 parsed
2026-08-18 11:29:02,572 [INFO] scraper: fetch_race 18/7: boats=6 odds=188/191
2026-08-18 11:29:02,575 [INFO] predictor: CALIBRATION_MODE=on
2026-08-18 11:29:02,575 [INFO] predictor: combos: {'win': 4, '2t': 29, '3t': 120}
2026-08-18 11:29:02,579 [INFO] run_cycle: fetched 18/7 [scan]: 153 combos
2026-08-18 11:29:02,806 [INFO] run_cycle: run_cycle done: 0 notifications

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
    "c": 88
  },
  {
    "target": "primary",
    "ok": 1,
    "c": 88
  }
]
```

## Phase別通知記録 (24h)
{'final': 36, 'result': 18, 'scan': 34}

## アラート件数 (24h・種類別)
```
  ANOMALY_SCRAPER_FAILURE_BURST: 109
  CIRCUIT_BREAKER_TRIP: 55
  CIRCUIT_BREAKER_NO_ACTION: 51
  ANOMALY_SCAN_FINAL_RATIO: 30
  FINAL_MISSING: 25
  STRATEGY_CI_FAIL: 17
  ANOMALY_BET_VOLUME_DROP: 2
  LARGE_ODDS_DRIFT: 1
```

## 戦略別 ROI (7日)
| sid | n | hits | cost | payout | PL | ROI |
|---|---|---|---|---|---|---|
| S00 | 43 | 9 | 12,900 | 7,470 | -5,430 | 0.579 |
| S01_NAKAANA1 | 47 | 12 | 9,400 | 7,520 | -1,880 | 0.8 |
| S02_TETSUBAN | 23 | 9 | 4,600 | 2,640 | -1,960 | 0.574 |

## 直近アラート (24h・新しい順)
```
[11:29:02] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 4, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1098}
[11:27:38] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 4, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1077}
[11:27:38] ANOMALY_SCAN_FINAL_RATIO: {"abs_drop": 0.334, "baseline_mean": 0.762, "baseline_stdev": 0.129, "kind": "ANOMALY_SCAN_FINAL_RATIO", "today_ratio": 0.429, "today_scan_count": 7, "z_score": -2.59}
[11:26:25] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 4, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1083}
[11:25:44] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 4, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1065}
[11:24:20] LARGE_ODDS_DRIFT: {"combo": "1", "drift_pct": -14.6, "final": 7.0, "kind": "LARGE_ODDS_DRIFT", "race": "147R", "scan": 8.2, "sid": "S00"}
[11:24:20] FINAL_MISSING: {"deadline": "2026-08-18T10:54:00+09:00", "kind": "FINAL_MISSING", "nid": "2026081814061054", "sid": "S00"}
[11:24:20] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 4, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1066}
[11:24:20] ANOMALY_SCAN_FINAL_RATIO: {"abs_drop": 0.262, "baseline_mean": 0.762, "baseline_stdev": 0.129, "kind": "ANOMALY_SCAN_FINAL_RATIO", "today_ratio": 0.5, "today_scan_count": 6, "z_score": -2.04}
[11:23:26] CIRCUIT_BREAKER_TRIP: {"cost": 4600, "kind": "CIRCUIT_BREAKER_TRIP", "n": 23, "payout": 2640, "roi_7d": 0.574, "sid": "S02_TETSUBAN"}
```

## 本日残レース: 112件

## 本日nidレジャー（ID単位完遂突合せ）
- race_schedule: 144件 登録 / 32件 締切済
- 通知発射: scan=7 nid / final=6 nid / result=2 nid
- predictions: 4 / うち結果DB記録済: 2
- ✅ 結果DBあるが通知未発射: 0件 `tools/backfill_result_notifications.py` で救済可
- 🔴 scan後final無しのまま締切: 3件（FINAL_MISSING の温床）

## 直近送信失敗 (24h)
```
```

## 最新 predictions サンプル (計算spot-check用)
| sid | race | bt | combo | p | odds | ev | bet | at |
|---|---|---|---|---|---|---|---|---|
| S00 | 147R | win | 1 | 0.5174 | 7.0 | 3.62 | 300 | scan=8.2 drift=-14.6% | 11:24:18 |
| S01_NAKAANA1 | 162R | win | 1 | 0.5334 | 3.5 | 1.87 | 200 | scan=- drift=- | 11:07:18 |
| S00 | 131R | win | 1 | 0.4111 | 4.2 | 1.73 | 300 | scan=- drift=- | 10:34:19 |
| S00 | 143R | win | 1 | 0.3177 | 4.7 | 1.49 | 300 | scan=- drift=- | 09:29:20 |
| S02_TETSUBAN | 2011R | win | 1 | 0.5735 | 2.5 | 1.43 | 200 | scan=- drift=- | 20:13:20 |
| S02_TETSUBAN | 203R | win | 1 | 0.4989 | 2.0 | 1.00 | 200 | scan=- drift=- | 16:19:20 |
| S02_TETSUBAN | 1312R | win | 1 | 0.5990 | 2.3 | 1.38 | 200 | scan=2.2 drift=+4.5% | 16:16:19 |
| S01_NAKAANA1 | 228R | win | 1 | 0.5735 | 3.7 | 2.12 | 200 | scan=- drift=- | 15:57:20 |
| S02_TETSUBAN | 058R | win | 1 | 0.5253 | 2.4 | 1.26 | 200 | scan=- drift=- | 15:05:19 |
| S00 | 058R | win | 1 | 0.5253 | 18.5 | 9.72 | 300 | scan=42.0 drift=-56.0% | 15:04:19 |

## オッズドリフト統計 (7日)

| bt | n | avg | min | max | down10 | collapse(≤-30%) | any_large(≥10%) |
|---|---|---|---|---|---|---|---|
| win | 69 | +3.6% | -62.9% | +207.5% | 19 | 9 | 35 |

## 校正テーブル合格状況

- total: 27 グループ
- passed: 19
- failed: 8 — `2f|4, 2f|5, 3f|2, 3f|3, 3f|4, 3t|1, 3t|4, 3t|5`
- 主力グループ状態: ✅ (全12グループ合格)

## SRE Golden Signals (24h)

| Signal | Value |
|---|---|
| **Latency** (scan→final avg) | 507.5s |
| **Latency** (scan→final max) | 602.3s |
| **Traffic** (notifications 24h) | 88 |
| **Errors** (send fail rate) | ✅ 0.0% |
| **Saturation** (S00) | 900円 used |
| **Saturation** (S01_NAKAANA1) | 200円 used |

## 信ぴょう性メトリクス（予測精度の証拠）

### bt別: 予測確率 vs 実的中率
| bt | n | 予測avg | 実的中率 | 校正誤差 | 過信度 | Brier |
|---|---|---|---|---|---|---|
| win | 409 | 0.4667 | 0.2714 | +0.1953 | 🟡+42% | 0.2369 |

### 戦略別: 校正精度 + Brier Skill Score
| sid | bt | n | pred | actual | Brier | BSS | ROI |
|---|---|---|---|---|---|---|---|
| S00 | win | 165 | 0.4162 | 0.2303 | 0.2208 | 🔴-0.25 | 0.658 |
| S01_NAKAANA1 | win | 171 | 0.4878 | 0.2222 | 0.2486 | 🔴-0.44 | 0.719 |
| S02_TETSUBAN | win | 73 | 0.5313 | 0.4795 | 0.2456 | ✅+0.02 | 0.741 |

### 確率デシル別: 校正カーブ
| 確率帯 | n | 予測avg | 実的中率 | gap |
|---|---|---|---|---|
| 0.10-0.15 | 9 | 0.1189 | 0.1111 | ✅+0.0078 |
| 0.15-0.20 | 11 | 0.1843 | 0.0909 | 🔴+0.0934 |
| 0.20-0.30 | 8 | 0.2246 | 0.3750 | 🔴-0.1504 |
| 0.30-0.50 | 154 | 0.4145 | 0.2273 | 🔴+0.1872 |
| 0.50+ | 225 | 0.5422 | 0.3156 | 🔴+0.2266 |

## Settlement Ratio データ品質

- 学習済み: 4バンド / fallback: 13バンド
| bt | odds帯 | source | n | ratio |
|---|---|---|---|---|
| win | <3.0 | ✅learned | 112 | 0.765 |
| win | <5.0 | ✅learned | 193 | 0.735 |
| win | <10.0 | ✅learned | 96 | 0.446 |
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
_auto-generated by claude_snapshot.py at 2026-08-18T11:30:01.615195+09:00_