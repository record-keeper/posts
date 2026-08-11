# ClaudeDebug スナップショット

## 🔴 現状: RED

**生成**: 2026-08-11T22:50:01.239288+09:00

### 次に取るべきアクション
> RED最優先: CRITICAL_ODDS_COLLAPSE×1 (24h) → ログ/DB確認

### 検出された問題
- 🟡 FINAL_MISSING×40 (24h)
- 🔴 CIRCUIT_BREAKER_TRIP×25 (24h)
- 🔴 STRATEGY_CI_FAIL×17 (24h)
- 🟡 LARGE_ODDS_DRIFT×2 (24h)
- 🔴 CRITICAL_ODDS_COLLAPSE×1 (24h)
- 🔴 alert_manager dispatch 失敗確定 1件（手動確認必要）

---

## 🔧 AI デバッグキュー（このClaudeが対処）

### 🔴 CIRCUIT_BREAKER_TRIP  ×40  [2026-08-11T22:10:07]
- key: `CIRCUIT_BREAKER_TRIP|`
- **FIX**: 7日ROI<0.7→戦略を enabled:false にして原因調査。校正ドリフトか市場変化を確認

### 🔴 CIRCUIT_BREAKER_NO_ACTION  ×80  [2026-08-11T22:10:07]
- key: `CIRCUIT_BREAKER_NO_ACTION|`
- **FIX**: CIRCUIT_BREAKER_TRIP 発動済なのに strategies.json で enabled のまま。enabled:false に切替 or 復旧条件満たしたか確認

### 🔴 STRATEGY_CI_FAIL  ×40  [2026-08-11T22:10:07]
- key: `STRATEGY_CI_FAIL|`
- **FIX**: grid戦略のOOS CI下限<1.0→論文基準で赤字リスク。strategies.json確認

### 🔴 CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION  ×3  [2026-08-11T21:30:02]
- key: `CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION|戦略 S00 が TRIP してるが enabled のまま`
- **FIX**: CIRCUIT_BREAKER_TRIP 戦略が enabled のまま。enabled:false に

### 🔴 CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION  ×3  [2026-08-11T21:30:02]
- key: `CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION|戦略 S01_NAKAANA1 が TRIP してるが enabled のまま`
- **FIX**: CIRCUIT_BREAKER_TRIP 戦略が enabled のまま。enabled:false に

### 🟡 ANOMALY_SCRAPER_FAILURE_BURST  ×25  [2026-08-11T18:18:30]
- key: `ANOMALY_SCRAPER_FAILURE_BURST|`
- **FIX**: 直近1h でscraper 3-retry 全敗多発。boatrace.jp 側timeout / IP ban / DDoS

### 🟡 ANOMALY_SCAN_FINAL_RATIO  ×24  [2026-08-11T11:54:44]
- key: `ANOMALY_SCAN_FINAL_RATIO|`
- **FIX**: scan→final成立率が7日baselineから2σ逸脱。scan/final window設定・odds取得タイミング

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-08-11T06:00:14]
- key: `INSUFFICIENT_SAMPLE|S02_TETSUBAN: n=67<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### 🟡 ORPHAN_SCAN  ×1  [2026-08-11T06:00:14]
- key: `ORPHAN_SCAN|173 件の scan に final/retreat 追従無し`
- **FIX**: scan 後 final も retreat も無い→当該レースの final 窓が短すぎ/fetch 失敗

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-08-11T06:00:14]
- key: `INSUFFICIENT_SAMPLE|S01_NAKAANA1: n=163<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ DRIFT_BUCKET  ×1  [2026-08-11T06:00:14]
- key: `DRIFT_BUCKET|drift ≤-30%: n=35 hit%=20.0% ROI=0.61 (コスト 10,300/回収 6,270)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ CALIBRATION_LIVE  ×1  [2026-08-11T06:00:14]
- key: `CALIBRATION_LIVE|decile 0.10-0.15: n=11 pred=0.1216 actual=0.1818 gap=-0.0602`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-08-11T06:00:14]
- key: `CALIBRATION_LIVE|decile 0.15-0.20: n=11 pred=0.1835 actual=0.1818 gap=+0.0017`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-08-11T06:00:14]
- key: `ROI_STAT|S00: n=171 hit%=22.8% hit_CI[Bonf]=[14.9,33.2]% ROI=0.67 ROI_boot95=[0.46,0.90]`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-08-11T06:00:14]
- key: `INSUFFICIENT_SAMPLE|S00: n=171<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ ROI_STAT  ×1  [2026-08-11T06:00:14]
- key: `ROI_STAT|S01_NAKAANA1: n=163 hit%=23.3% hit_CI[Bonf]=[15.2,34.0]% ROI=0.70 ROI_boot95=[0.`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-08-11T06:00:14]
- key: `ROI_STAT|S02_TETSUBAN: n=67 hit%=50.7% hit_CI[Bonf]=[34.0,67.3]% ROI=0.87 ROI_boot95=[0.6`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ DRIFT_BUCKET  ×1  [2026-08-11T06:00:14]
- key: `DRIFT_BUCKET|drift -30%〜-10%: n=35 hit%=34.3% ROI=0.82 (コスト 8,600/回収 7,060)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-08-11T06:00:14]
- key: `DRIFT_BUCKET|drift -10%〜+10%: n=64 hit%=25.0% ROI=0.68 (コスト 15,100/回収 10,250)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-08-11T06:00:14]
- key: `DRIFT_BUCKET|drift +10%〜+30%: n=50 hit%=24.0% ROI=0.49 (コスト 11,600/回収 5,640)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料


以下、詳細セクション（通常読み飛ばし可）

## 環境・コード状態
- git_sha: `<error: Command '['git', '-C', '/opt/boa` dirty=True
- config.json md5: `eb532e851a30cd2f7e69bdf0dfca3f2b`
- strategies.json md5: `06b22dd935785e7947bf9c0f170b69a3`
- numpy=2.4.4 lightgbm=4.6.0 scipy=1.17.1
- **calibration_applied**: True ← predictor.py が校正を呼んでるか
- DB: 10.14MB / last modified 2026-08-11T22:49:04.313769+09:00

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
16 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-08-11 22:45:03,816 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-08-11 22:45:03,850 [INFO] predictor: Models loaded OK
2026-08-11 22:45:03,853 [INFO] run_cycle: run_cycle done: 0 notifications
2026-08-11 22:46:03,674 [INFO] run_cycle: === run_cycle 22:46:03 ===
2026-08-11 22:46:03,674 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-08-11 22:46:03,674 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-08-11 22:46:03,724 [INFO] predictor: Models loaded OK
2026-08-11 22:46:03,727 [INFO] run_cycle: run_cycle done: 0 notifications
2026-08-11 22:47:04,007 [INFO] run_cycle: === run_cycle 22:47:04 ===
2026-08-11 22:47:04,007 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-08-11 22:47:04,007 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-08-11 22:47:04,061 [INFO] predictor: Models loaded OK
2026-08-11 22:47:04,066 [INFO] run_cycle: run_cycle done: 0 notifications
2026-08-11 22:48:03,562 [INFO] run_cycle: === run_cycle 22:48:03 ===
2026-08-11 22:48:03,562 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-08-11 22:48:03,562 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-08-11 22:48:03,596 [INFO] predictor: Models loaded OK
2026-08-11 22:48:03,599 [INFO] run_cycle: run_cycle done: 0 notifications
2026-08-11 22:49:03,914 [INFO] run_cycle: === run_cycle 22:49:03 ===
2026-08-11 22:49:03,914 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-08-11 22:49:03,914 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-08-11 22:49:03,966 [INFO] predictor: Models loaded OK
2026-08-11 22:49:03,971 [INFO] run_cycle: run_cycle done: 0 notifications

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
    "c": 100
  },
  {
    "target": "primary",
    "ok": 1,
    "c": 100
  }
]
```

## Phase別通知記録 (24h)
{'final': 41, 'result': 20, 'scan': 39}

## アラート件数 (24h・種類別)
```
  ANOMALY_SCRAPER_FAILURE_BURST: 65
  FINAL_MISSING: 40
  CIRCUIT_BREAKER_NO_ACTION: 34
  CIRCUIT_BREAKER_TRIP: 25
  STRATEGY_CI_FAIL: 17
  ANOMALY_SCAN_FINAL_RATIO: 6
  LARGE_ODDS_DRIFT: 2
  CRITICAL_ODDS_COLLAPSE: 1
```

## 戦略別 ROI (7日)
| sid | n | hits | cost | payout | PL | ROI |
|---|---|---|---|---|---|---|
| S00 | 34 | 9 | 10,200 | 8,700 | -1,500 | 0.853 |
| S01_NAKAANA1 | 48 | 10 | 9,600 | 5,800 | -3,800 | 0.604 |
| S02_TETSUBAN | 18 | 11 | 3,600 | 3,360 | -240 | 0.933 |

## 直近アラート (24h・新しい順)
```
[22:34:04] CIRCUIT_BREAKER_TRIP: {"cost": 9600, "kind": "CIRCUIT_BREAKER_TRIP", "n": 48, "payout": 5800, "roi_7d": 0.604, "sid": "S01_NAKAANA1"}
[22:20:20] FINAL_MISSING: {"deadline": "2026-08-11T12:45:00+09:00", "kind": "FINAL_MISSING", "nid": "2026081113061245", "sid": "S00"}
[22:17:19] FINAL_MISSING: {"deadline": "2026-08-11T16:43:00+09:00", "kind": "FINAL_MISSING", "nid": "2026081107041643", "sid": "S00"}
[22:15:04] FINAL_MISSING: {"deadline": "2026-08-11T17:42:00+09:00", "kind": "FINAL_MISSING", "nid": "2026081104121742", "sid": "S00"}
[22:10:05] STRATEGY_CI_FAIL: {"ci_lo": null, "kind": "STRATEGY_CI_FAIL", "sid": "S02_TETSUBAN"}
[22:10:05] CIRCUIT_BREAKER_NO_ACTION: {"kind": "CIRCUIT_BREAKER_NO_ACTION", "sid": "S01_NAKAANA1"}
[22:10:05] CIRCUIT_BREAKER_NO_ACTION: {"kind": "CIRCUIT_BREAKER_NO_ACTION", "sid": "S00"}
[22:08:05] FINAL_MISSING: {"deadline": "2026-08-11T13:33:00+09:00", "kind": "FINAL_MISSING", "nid": "2026081105051333", "sid": "S00"}
[21:33:04] CIRCUIT_BREAKER_TRIP: {"cost": 9600, "kind": "CIRCUIT_BREAKER_TRIP", "n": 48, "payout": 5800, "roi_7d": 0.604, "sid": "S01_NAKAANA1"}
[21:19:04] FINAL_MISSING: {"deadline": "2026-08-11T12:45:00+09:00", "kind": "FINAL_MISSING", "nid": "2026081113061245", "sid": "S00"}
```

## 本日残レース: 0件

## 本日nidレジャー（ID単位完遂突合せ）
- race_schedule: 180件 登録 / 180件 締切済
- 通知発射: scan=35 nid / final=37 nid / result=19 nid
- predictions: 20 / うち結果DB記録済: 20
- ✅ 結果DBあるが通知未発射: 0件 `tools/backfill_result_notifications.py` で救済可
- 🔴 scan後final無しのまま締切: 4件（FINAL_MISSING の温床）

## 直近送信失敗 (24h)
```
```

## 最新 predictions サンプル (計算spot-check用)
| sid | race | bt | combo | p | odds | ev | bet | at |
|---|---|---|---|---|---|---|---|---|
| S02_TETSUBAN | 079R | win | 1 | 0.4989 | 2.6 | 1.30 | 200 | scan=2.5 drift=+4.0% | 19:08:19 |
| S01_NAKAANA1 | 194R | win | 1 | 0.5990 | 4.0 | 2.40 | 200 | scan=- drift=- | 19:00:46 |
| S02_TETSUBAN | 208R | win | 1 | 0.5334 | 2.0 | 1.07 | 200 | scan=2.1 drift=-4.8% | 18:43:29 |
| S02_TETSUBAN | 076R | win | 1 | 0.5174 | 2.3 | 1.19 | 200 | scan=- drift=- | 17:33:45 |
| S02_TETSUBAN | 0512R | win | 1 | 0.4989 | 2.5 | 1.25 | 200 | scan=2.4 drift=+4.2% | 17:22:36 |
| S01_NAKAANA1 | 074R | win | 1 | 0.5891 | 3.7 | 2.18 | 200 | scan=3.2 drift=+15.6% | 16:40:45 |
| S00 | 073R | win | 1 | 0.5174 | 6.1 | 3.16 | 300 | scan=4.0 drift=+52.5% | 16:13:25 |
| S01_NAKAANA1 | 1811R | win | 1 | 0.4989 | 3.0 | 1.50 | 200 | scan=4.4 drift=-31.8% | 15:50:34 |
| S00 | 068R | win | 1 | 0.6037 | 4.7 | 2.84 | 300 | scan=5.5 drift=-14.5% | 14:58:19 |
| S01_NAKAANA1 | 166R | win | 1 | 0.5123 | 4.0 | 2.05 | 200 | scan=4.6 drift=-13.0% | 13:16:21 |

## オッズドリフト統計 (7日)

| bt | n | avg | min | max | down10 | collapse(≤-30%) | any_large(≥10%) |
|---|---|---|---|---|---|---|---|
| win | 64 | +7.2% | -53.3% | +287.7% | 20 | 8 | 43 |

## 校正テーブル合格状況

- total: 27 グループ
- passed: 19
- failed: 8 — `2f|4, 2f|5, 3f|2, 3f|3, 3f|4, 3t|1, 3t|4, 3t|5`
- 主力グループ状態: ✅ (全12グループ合格)

## SRE Golden Signals (24h)

| Signal | Value |
|---|---|
| **Latency** (scan→final avg) | 447.2s |
| **Latency** (scan→final max) | 616.7s |
| **Traffic** (notifications 24h) | 100 |
| **Errors** (send fail rate) | ✅ 0.0% |
| **Saturation** (S00) | 1,200円 used |
| **Saturation** (S01_NAKAANA1) | 2,200円 used |
| **Saturation** (S02_TETSUBAN) | 1,000円 used |

## 信ぴょう性メトリクス（予測精度の証拠）

### bt別: 予測確率 vs 実的中率
| bt | n | 予測avg | 実的中率 | 校正誤差 | 過信度 | Brier |
|---|---|---|---|---|---|---|
| win | 398 | 0.4672 | 0.2739 | +0.1933 | 🟡+41% | 0.2365 |

### 戦略別: 校正精度 + Brier Skill Score
| sid | bt | n | pred | actual | Brier | BSS | ROI |
|---|---|---|---|---|---|---|---|
| S00 | win | 162 | 0.4196 | 0.2222 | 0.2244 | 🔴-0.30 | 0.627 |
| S01_NAKAANA1 | win | 167 | 0.4869 | 0.2216 | 0.2466 | 🔴-0.43 | 0.68 |
| S02_TETSUBAN | win | 69 | 0.5311 | 0.5217 | 0.2407 | ✅+0.04 | 0.887 |

### 確率デシル別: 校正カーブ
| 確率帯 | n | 予測avg | 実的中率 | gap |
|---|---|---|---|---|
| 0.10-0.15 | 11 | 0.1216 | 0.1818 | 🔴-0.0602 |
| 0.15-0.20 | 10 | 0.1843 | 0.1000 | 🔴+0.0843 |
| 0.20-0.30 | 9 | 0.2243 | 0.3333 | 🔴-0.1091 |
| 0.30-0.50 | 152 | 0.4195 | 0.2237 | 🔴+0.1958 |
| 0.50+ | 215 | 0.5436 | 0.3209 | 🔴+0.2226 |

## Settlement Ratio データ品質

- 学習済み: 4バンド / fallback: 13バンド
| bt | odds帯 | source | n | ratio |
|---|---|---|---|---|
| win | <3.0 | ✅learned | 106 | 0.776 |
| win | <5.0 | ✅learned | 181 | 0.725 |
| win | <10.0 | ✅learned | 91 | 0.451 |
| win | <20.0 | ✅learned | 30 | 0.227 |
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
_auto-generated by claude_snapshot.py at 2026-08-11T22:50:01.239288+09:00_