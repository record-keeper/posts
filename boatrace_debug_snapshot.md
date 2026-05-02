# ClaudeDebug スナップショット

## 🔴 現状: RED

**生成**: 2026-05-02T23:30:02.048176+09:00

### 次に取るべきアクション
> RED最優先: CALIBRATION_DRIFT×29 (24h) → ログ/DB確認

### 検出された問題
- 🟡 FINAL_MISSING×88 (24h)
- 🔴 CALIBRATION_DRIFT×29 (24h)
- 🔴 CIRCUIT_BREAKER_TRIP×15 (24h)
- 🟡 LARGE_ODDS_DRIFT×1 (24h)

---

## 🔧 AI デバッグキュー（このClaudeが対処）

### 🔴 CIRCUIT_BREAKER_TRIP  ×3  [2026-05-02T23:27:06]
- key: `CIRCUIT_BREAKER_TRIP|`
- **FIX**: 7日ROI<0.7→戦略を enabled:false にして原因調査。校正ドリフトか市場変化を確認

### 🔴 CIRCUIT_BREAKER_NO_ACTION  ×21  [2026-05-02T23:09:06]
- key: `CIRCUIT_BREAKER_NO_ACTION|`
- **FIX**: CIRCUIT_BREAKER_TRIP 発動済なのに strategies.json で enabled のまま。enabled:false に切替 or 復旧条件満たしたか確認

### 🔴 CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION  ×2  [2026-05-02T23:00:05]
- key: `CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION|戦略 S00 が TRIP してるが enabled のまま`
- **FIX**: CIRCUIT_BREAKER_TRIP 戦略が enabled のまま。enabled:false に

### 🔴 CALIBRATION_DRIFT  ×60  [2026-05-02T22:30:09]
- key: `CALIBRATION_DRIFT|`
- **FIX**: 予測確率が実的中率から50%以上乖離→isotonic_calibration.json 再生成 or モデル再学習が必要。EV計算が膨張中

### 🟡 CODE_AUDIT_SCRAPER_FAILURE_RATE_HIGH  ×1  [2026-05-02T20:30:03]
- key: `CODE_AUDIT_SCRAPER_FAILURE_RATE_HIGH|直近 500 log行 で 3-retry 全敗 4 件 (閾値 3)`
- **FIX**: scraper 3-retry 全敗多発。boatrace.jp timeout or IP ban 疑い

### 🟡 ANOMALY_SCRAPER_FAILURE_BURST  ×47  [2026-05-02T20:22:41]
- key: `ANOMALY_SCRAPER_FAILURE_BURST|`
- **FIX**: 直近1h でscraper 3-retry 全敗多発。boatrace.jp 側timeout / IP ban / DDoS

### 🟡 ANOMALY_BET_VOLUME_SPIKE  ×9  [2026-05-02T19:50:25]
- key: `ANOMALY_BET_VOLUME_SPIKE|`
- **FIX**: 本日のbet数が2σ急増。filter logic緩み・戦略追加・race_schedule異常

### 🟡 ANOMALY_SCAN_FINAL_RATIO  ×10  [2026-05-02T12:55:53]
- key: `ANOMALY_SCAN_FINAL_RATIO|`
- **FIX**: scan→final成立率が7日baselineから2σ逸脱。scan/final window設定・odds取得タイミング

### ℹ️ CALIBRATION_LIVE  ×1  [2026-05-02T06:00:08]
- key: `CALIBRATION_LIVE|decile 0.30-0.40: n=6 pred=0.3241 actual=0.0000 gap=+0.3241`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-05-02T06:00:08]
- key: `ROI_STAT|S00: n=84 hit%=22.6% hit_CI[Bonf]=[12.3,37.9]% ROI=0.78 ROI_boot95=[0.43,1.17]`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-05-02T06:00:08]
- key: `INSUFFICIENT_SAMPLE|S00: n=84<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### 🟡 ORPHAN_SCAN  ×1  [2026-05-02T06:00:08]
- key: `ORPHAN_SCAN|72 件の scan に final/retreat 追従無し`
- **FIX**: scan 後 final も retreat も無い→当該レースの final 窓が短すぎ/fetch 失敗

### ℹ️ CALIBRATION_LIVE  ×1  [2026-05-02T06:00:08]
- key: `CALIBRATION_LIVE|bt=win: n=84 pred=0.4340 actual=0.2262 error=+0.2078 (+48%) brier=0.2322 [OVERCO`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-05-02T06:00:08]
- key: `CALIBRATION_LIVE|S00(win): n=84 pred=0.4340 hit=0.2262 cal_err=+0.2078 brier=0.2322 BSS=-0.33 ROI`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-05-02T06:00:08]
- key: `CALIBRATION_LIVE|decile 0.20-0.30: n=5 pred=0.2201 actual=0.4000 gap=-0.1799`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-05-02T06:00:08]
- key: `CALIBRATION_LIVE|decile 0.40-0.50: n=35 pred=0.4472 actual=0.2286 gap=+0.2187`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-05-02T06:00:08]
- key: `CALIBRATION_LIVE|decile 0.50+: n=32 pred=0.5335 actual=0.2500 gap=+0.2835`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### 🟡 PAYOUT_RATIO_WEIRD  ×1  [2026-05-02T06:00:07]
- key: `PAYOUT_RATIO_WEIRD|pid=759 bet=300 odds=4.0 payout=1980 ratio=1.65`
- **FIX**: 同着分割 or 直前オッズ崩落の実現象。CRITICAL ではない、件数のみ監視

### 🟡 PAYOUT_RATIO_WEIRD  ×1  [2026-05-02T06:00:07]
- key: `PAYOUT_RATIO_WEIRD|pid=881 bet=300 odds=12.7 payout=900 ratio=0.24`
- **FIX**: 同着分割 or 直前オッズ崩落の実現象。CRITICAL ではない、件数のみ監視

### 🟡 PAYOUT_RATIO_WEIRD  ×1  [2026-05-02T06:00:07]
- key: `PAYOUT_RATIO_WEIRD|pid=906 bet=300 odds=14.2 payout=360 ratio=0.08`
- **FIX**: 同着分割 or 直前オッズ崩落の実現象。CRITICAL ではない、件数のみ監視


以下、詳細セクション（通常読み飛ばし可）

## 環境・コード状態
- git_sha: `<error: Command '['git', '-C', '/opt/boa` dirty=True
- config.json md5: `eb532e851a30cd2f7e69bdf0dfca3f2b`
- strategies.json md5: `149bfa9ecc7e714a646f5a33d43fea95`
- numpy=2.4.4 lightgbm=4.6.0 scipy=1.17.1
- **calibration_applied**: True ← predictor.py が校正を呼んでるか
- DB: 1.62MB / last modified 2026-05-02T23:30:03.512711+09:00

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
81 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-05-02 23:25:06,381 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-05-02 23:25:06,449 [INFO] predictor: Models loaded OK
2026-05-02 23:25:06,745 [INFO] run_cycle: run_cycle done: 0 notifications
2026-05-02 23:26:05,994 [INFO] run_cycle: === run_cycle 23:26:05 ===
2026-05-02 23:26:05,995 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-05-02 23:26:05,995 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-05-02 23:26:06,098 [INFO] predictor: Models loaded OK
2026-05-02 23:26:06,104 [INFO] run_cycle: run_cycle done: 0 notifications
2026-05-02 23:27:05,956 [INFO] run_cycle: === run_cycle 23:27:05 ===
2026-05-02 23:27:05,956 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-05-02 23:27:05,956 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-05-02 23:27:06,000 [INFO] predictor: Models loaded OK
2026-05-02 23:27:06,004 [INFO] run_cycle: run_cycle done: 0 notifications
2026-05-02 23:28:06,045 [INFO] run_cycle: === run_cycle 23:28:06 ===
2026-05-02 23:28:06,045 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-05-02 23:28:06,045 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-05-02 23:28:06,088 [INFO] predictor: Models loaded OK
2026-05-02 23:28:06,093 [INFO] run_cycle: run_cycle done: 0 notifications
2026-05-02 23:29:05,950 [INFO] run_cycle: === run_cycle 23:29:05 ===
2026-05-02 23:29:05,950 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-05-02 23:29:05,950 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-05-02 23:29:05,995 [INFO] predictor: Models loaded OK
2026-05-02 23:29:06,000 [INFO] run_cycle: run_cycle done: 0 notifications

```

## 戦略有効/無効一覧
| id | trust | bt | ev_th | pmin | enabled |
|---|---|---|---|---|---|
| S00 | S | win | 4.0 | 0.0 | True |

## Webhook送信 (24h)
```
[
  {
    "target": "mirror",
    "ok": 1,
    "c": 41
  },
  {
    "target": "primary",
    "ok": 1,
    "c": 41
  }
]
```

## Phase別通知記録 (24h)
{'final': 12, 'result': 11, 'scan': 18}

## アラート件数 (24h・種類別)
```
  ANOMALY_SCRAPER_FAILURE_BURST: 242
  FINAL_MISSING: 88
  CALIBRATION_DRIFT: 29
  CIRCUIT_BREAKER_NO_ACTION: 17
  CIRCUIT_BREAKER_TRIP: 15
  ANOMALY_BET_VOLUME_SPIKE: 5
  ANOMALY_SCAN_FINAL_RATIO: 2
  LARGE_ODDS_DRIFT: 1
```

## 戦略別 ROI (7日)
| sid | n | hits | cost | payout | PL | ROI |
|---|---|---|---|---|---|---|
| S00 | 48 | 9 | 14,400 | 9,930 | -4,470 | 0.69 |

## 直近アラート (24h・新しい順)
```
[23:26:06] CIRCUIT_BREAKER_TRIP: {"cost": 14400, "kind": "CIRCUIT_BREAKER_TRIP", "n": 48, "payout": 9930, "roi_7d": 0.69, "sid": "S00"}
[23:24:05] CALIBRATION_DRIFT: {"avg_actual": 0.1875, "avg_pred": 0.4226, "bt": "win", "kind": "CALIBRATION_DRIFT", "n": 48, "overconf_pct": 55.6}
[23:19:06] FINAL_MISSING: {"deadline": "2026-05-02T09:42:00+09:00", "kind": "FINAL_MISSING", "nid": "2026050214030942", "sid": "S00"}
[23:13:06] FINAL_MISSING: {"deadline": "2026-05-02T12:38:00+09:00", "kind": "FINAL_MISSING", "nid": "2026050214091238", "sid": "S00"}
[23:13:06] FINAL_MISSING: {"deadline": "2026-05-02T12:36:00+09:00", "kind": "FINAL_MISSING", "nid": "2026050210091236", "sid": "S00"}
[23:13:06] CIRCUIT_BREAKER_NO_ACTION: {"kind": "CIRCUIT_BREAKER_NO_ACTION", "sid": "S00"}
[23:09:06] FINAL_MISSING: {"deadline": "2026-05-02T14:36:00+09:00", "kind": "FINAL_MISSING", "nid": "2026050205061436", "sid": "S00"}
[23:02:06] FINAL_MISSING: {"deadline": "2026-05-02T12:25:00+09:00", "kind": "FINAL_MISSING", "nid": "2026050223091225", "sid": "S00"}
[23:01:05] FINAL_MISSING: {"deadline": "2026-05-02T16:26:00+09:00", "kind": "FINAL_MISSING", "nid": "2026050207031626", "sid": "S00"}
[22:57:06] FINAL_MISSING: {"deadline": "2026-05-02T13:20:00+09:00", "kind": "FINAL_MISSING", "nid": "2026050209071320", "sid": "S00"}
```

## 本日残レース: 0件

## 本日nidレジャー（ID単位完遂突合せ）
- race_schedule: 180件 登録 / 180件 締切済
- 通知発射: scan=18 nid / final=12 nid / result=11 nid
- predictions: 11 / うち結果DB記録済: 11
- ✅ 結果DBあるが通知未発射: 0件 `tools/backfill_result_notifications.py` で救済可
- 🔴 scan後final無しのまま締切: 8件（FINAL_MISSING の温床）

## 直近送信失敗 (24h)
```
```

## 最新 predictions サンプル (計算spot-check用)
| sid | race | bt | combo | p | odds | ev | bet | at |
|---|---|---|---|---|---|---|---|---|
| S00 | 076R | win | 1 | 0.2290 | 6.0 | 1.37 | 300 | scan=4.0 drift=+50.0% | 17:48:32 |
| S00 | 072R | win | 1 | 0.1957 | 7.6 | 1.49 | 300 | scan=40.8 drift=-81.4% | 15:54:45 |
| S00 | 178R | win | 1 | 0.3177 | 45.7 | 14.52 | 300 | scan=- drift=- | 14:33:32 |
| S00 | 167R | win | 1 | 0.4989 | 4.9 | 2.44 | 300 | scan=4.7 drift=+4.3% | 14:06:44 |
| S00 | 176R | win | 1 | 0.1957 | 6.7 | 1.31 | 300 | scan=7.5 drift=-10.7% | 13:19:45 |
| S00 | 1010R | win | 1 | 0.4111 | 6.4 | 2.63 | 300 | scan=18.7 drift=-65.8% | 13:05:46 |
| S00 | 108R | win | 1 | 0.2290 | 4.8 | 1.10 | 300 | scan=- drift=- | 11:57:32 |
| S00 | 023R | win | 1 | 0.5572 | 4.7 | 2.62 | 300 | scan=4.7 drift=+0.0% | 11:42:20 |
| S00 | 147R | win | 1 | 0.5476 | 4.6 | 2.52 | 300 | scan=4.4 drift=+4.5% | 11:31:21 |
| S00 | 145R | win | 1 | 0.5123 | 7.1 | 3.64 | 300 | scan=4.1 drift=+73.2% | 10:31:21 |

## オッズドリフト統計 (7日)

| bt | n | avg | min | max | down10 | collapse(≤-30%) | any_large(≥10%) |
|---|---|---|---|---|---|---|---|
| win | 34 | -3.2% | -81.4% | +117.3% | 14 | 9 | 25 |

## 校正テーブル合格状況

- total: 27 グループ
- passed: 19
- failed: 8 — `2f|4, 2f|5, 3f|2, 3f|3, 3f|4, 3t|1, 3t|4, 3t|5`
- 主力グループ状態: ✅ (全12グループ合格)

## SRE Golden Signals (24h)

| Signal | Value |
|---|---|
| **Latency** (scan→final avg) | 558.8s |
| **Latency** (scan→final max) | 616.9s |
| **Traffic** (notifications 24h) | 41 |
| **Errors** (send fail rate) | ✅ 0.0% |
| **Saturation** (S00) | 3,300円 used |

## 信ぴょう性メトリクス（予測精度の証拠）

### bt別: 予測確率 vs 実的中率
| bt | n | 予測avg | 実的中率 | 校正誤差 | 過信度 | Brier |
|---|---|---|---|---|---|---|
| win | 95 | 0.4279 | 0.2211 | +0.2068 | 🟡+48% | 0.2309 |

### 戦略別: 校正精度 + Brier Skill Score
| sid | bt | n | pred | actual | Brier | BSS | ROI |
|---|---|---|---|---|---|---|---|
| S00 | win | 95 | 0.4279 | 0.2211 | 0.2309 | 🔴-0.34 | 0.834 |

### 確率デシル別: 校正カーブ
| 確率帯 | n | 予測avg | 実的中率 | gap |
|---|---|---|---|---|
| 0.20-0.30 | 7 | 0.2227 | 0.2857 | 🔴-0.0630 |
| 0.30-0.50 | 45 | 0.4294 | 0.2000 | 🔴+0.2294 |
| 0.50+ | 35 | 0.5340 | 0.2286 | 🔴+0.3054 |

## Settlement Ratio データ品質

- 学習済み: 1バンド / fallback: 15バンド
| bt | odds帯 | source | n | ratio |
|---|---|---|---|---|
| win | <3.0 | ⚠️fallback | 0 | 0.4 |
| win | <5.0 | ⚠️fallback | 5 | 0.35 |
| win | <10.0 | ✅learned | 14 | 0.589 |
| win | <20.0 | ⚠️fallback | 2 | 0.22 |
| win | <50.0 | ⚠️fallback | 0 | 0.1 |
| win | ∞ | ⚠️fallback | 0 | 0.1 |
| 2t | <10.0 | ⚠️fallback | 0 | 0.5 |
| 2t | <30.0 | ⚠️fallback | 0 | 0.35 |
| 2t | ∞ | ⚠️fallback | 0 | 0.25 |
| 3t | <50.0 | ⚠️fallback | 0 | 0.4 |
| 3t | <200.0 | ⚠️fallback | 0 | 0.3 |
| 3t | ∞ | ⚠️fallback | 0 | 0.2 |
| 2f | <10.0 | ⚠️fallback | 0 | 0.45 |
| 2f | ∞ | ⚠️fallback | 0 | 0.3 |
| 3f | <50.0 | ⚠️fallback | 0 | 0.4 |
| 3f | ∞ | ⚠️fallback | 0 | 0.25 |

---
_auto-generated by claude_snapshot.py at 2026-05-02T23:30:02.048176+09:00_